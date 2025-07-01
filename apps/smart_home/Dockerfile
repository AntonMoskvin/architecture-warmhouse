# Используем официальный образ с Go
FROM golang:1.22 as builder

# Устанавливаем рабочую директорию внутри контейнера
WORKDIR /app

# Копируем только go.mod и go.sum для восстановления модулей
COPY go.mod .
COPY go.sum .

# Скачиваем зависимости
RUN go mod download

# Копируем весь исходный код
COPY . .

# Собираем бинарник
RUN CGO_ENABLED=0 GOOS=linux go build -o /smarthome

# Финальный образ без Go
FROM gcr.io/distroless/base-debian12

# Копируем бинарник из builder
COPY --from=builder /smarthome /smarthome

# Запускаем приложение
CMD ["/smarthome"]