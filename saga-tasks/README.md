# Checkout Saga - Task Index

## Muc dich

Thu muc nay dung de giao viec cho tung nhom phu trach khi chuyen flow checkout sang mo hinh **Saga Orchestrator + RabbitMQ**.

Tai lieu tong quan kien truc nam tai:

- `../../ai-agent-saga/checkout-saga-orchestrator-rabbitmq-flow.md`

Moi file trong thu muc nay tuong ung voi mot service can sua. Cau truc moi file deu theo thu tu:

1. Tong quan
2. Nhiem vu cu the
3. Minh hoa

## Thu tu trien khai de xuat

1. `bookstore-order-service`
2. `bookstore-book-service`
3. `bookstore-promotion-service`
4. `bookstore-payment-service`
5. `bookstore-shipping-service`
6. `bookstore-cart-service`
7. `bookstore-notification-service`
8. `bookstore-api-gateway`
9. Kiem tra lai `bookstore-saga-orchestrator-service`

Ly do cua thu tu nay:

- `order-service` va `book-service` mo khoa flow nghiep vu chinh.
- `payment-service` va `shipping-service` quyet dinh duoc flow online payment va compensation.
- `cart-service`, `notification-service`, `api-gateway` la cac diem noi sau cung.

## Danh sach file task

- `bookstore-api-gateway.md`
- `bookstore-saga-orchestrator-service.md`
- `bookstore-order-service.md`
- `bookstore-book-service.md`
- `bookstore-promotion-service.md`
- `bookstore-payment-service.md`
- `bookstore-shipping-service.md`
- `bookstore-cart-service.md`
- `bookstore-notification-service.md`

## Service khong can thay doi lon trong phase nay

- `bookstore-user-service`: van cung cap du lieu doc dong bo nhu dia chi va thong tin user.
- `bookstore-review-service`
- `bookstore-news-service`
- `bookstore-ai-service`

Nhung service tren khong nam trong transaction checkout nen khong can dua vao saga.
