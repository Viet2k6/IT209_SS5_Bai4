# Bài 4: Mô phỏng quy trình Hotfix & Gitflow thực tế

## 1. Mục tiêu

Mô phỏng quy trình Gitflow khi hệ thống production trên nhánh `main` gặp lỗi nghiêm trọng cần sửa gấp.

## 2. Quy trình thực hiện

### Bước 1: Tạo phiên bản stable

Tạo commit ban đầu trên nhánh `main`:

```text
bb21b1f Initial release v1.0.0
```

Sau đó tạo nhánh `develop` để phát triển các tính năng mới.

### Bước 2: Tạo nhánh Hotfix

Chuyển từ `develop` về `main` và tạo nhánh:

```text
hotfix/v1.0.1
```

Nhánh này được tách trực tiếp từ `main`.

### Bước 3: Sửa lỗi

Thực hiện sửa lỗi bảo mật và tạo commit:

```text
f2e1a61 Fix security issue in v1.0.1
```

### Bước 4: Merge vào main và tạo tag

Merge nhánh `hotfix/v1.0.1` vào `main`, sau đó tạo tag:

```text
v1.0.1
```

Tag `v1.0.1` trỏ tới commit sửa lỗi `f2e1a61`.

### Bước 5: Merge ngược vào develop

Chuyển sang `develop` và merge nhánh `hotfix/v1.0.1` để đảm bảo lỗi đã được sửa trong phiên bản phát triển tương lai.

### Bước 6: Xóa nhánh Hotfix

Sau khi hoàn tất việc merge, xóa nhánh hotfix cục bộ:

```bash
git branch -d hotfix/v1.0.1
```

## 3. Sơ đồ Gitflow

```text
                    ┌── tag v1.0.1
                    │
main ── bb21b1f ─── f2e1a61
          │             │
          │             │
develop ──┘─────────────┘
                       ↑
                 hotfix/v1.0.1
```

Sau khi hoàn tất, nhánh `hotfix/v1.0.1` được xóa.

## 4. Kết quả kiểm tra

Lệnh:

```bash
git branch -a
```

Kết quả:

```text
* develop
  main
```

Lệnh:

```bash
git tag
```

Kết quả:

```text
v1.0.1
```

Lệnh:

```bash
git log --graph --oneline --all
```

Kết quả:

```text
* f2e1a61 (HEAD -> develop, tag: v1.0.1, main) Fix security issue in v1.0.1
* bb21b1f Initial release v1.0.0
```

## 5. Kết luận

Đã hoàn thành quy trình Hotfix theo Gitflow: tạo hotfix từ `main`, sửa lỗi, merge vào `main`, tạo tag `v1.0.1`, sau đó đồng bộ bản sửa lỗi về `develop`.
