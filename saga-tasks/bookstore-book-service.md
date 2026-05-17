# Task: bookstore-book-service

## 1. Tong quan

`bookstore-book-service` la noi duy nhat duoc phep quyet dinh ton kho co du hay khong. RabbitMQ chi truyen message; phep tru/giu kho that su phai duoc chot bang transaction trong database cua `book-service`.

Trong saga moi, stock khong duoc "tru ngay". No can di theo flow:

- `reserve`
- `confirm`
- `release`

## 2. Nhiem vu cu the

1. Bo sung mo hinh ton kho:
   - `on_hand_stock`
   - `reserved_stock`
   - `available_stock = on_hand_stock - reserved_stock`
2. Tao bang `stock_reservation`:
   - `reservation_id`
   - `saga_id`
   - `order_id`
   - `book_id`
   - `quantity`
   - `status`
   - `expires_at`
3. Tao consumer cho:
   - `book.stock.reserve.command`
   - `book.stock.confirm.command`
   - `book.stock.release.command`
4. Khi reserve:
   - dung atomic update trong transaction,
   - neu du hang thi tang `reserved_stock`,
   - neu khong du hang thi publish `book.stock.failed`.
5. Khi confirm:
   - giam `reserved_stock`,
   - giam `on_hand_stock`,
   - publish `book.stock.confirmed`.
6. Khi release:
   - giam `reserved_stock`,
   - khong doi `on_hand_stock`,
   - publish `book.stock.released`.
7. Moi lan ton kho thay doi, publish them `book.stock.changed` de phuc vu cache/read model/realtime UI.
8. Them timeout job giai phong reservation qua han.
9. Them idempotency:
   - mot `sagaId + bookId` chi reserve mot lan,
   - confirm/release lap lai khong duoc lam sai kho.

## 3. Minh hoa

Vi du ton kho ban dau:

```text
on_hand_stock = 10
reserved_stock = 3
available_stock = 7
```

User checkout 2 cuon:

```text
reserve:
on_hand_stock = 10
reserved_stock = 5
available_stock = 5
```

Thanh toan thanh cong:

```text
confirm:
on_hand_stock = 8
reserved_stock = 3
available_stock = 5
```

SQL atomic goi y:

```sql
UPDATE books
SET reserved_stock = reserved_stock + :quantity
WHERE id = :bookId
  AND (on_hand_stock - reserved_stock) >= :quantity;
```
