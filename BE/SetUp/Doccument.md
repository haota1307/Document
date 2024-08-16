# Cấu trúc thư mục dự án

Cấu trúc thư mục dự án mình sẽ sử dụng như sau:

```TXT
📦nodejs-typescript
 ┣ 📂dist
 ┣ 📂src
 ┃ ┣ 📂constants
 ┃ ┃ ┣ 📜enum.ts
 ┃ ┃ ┣ 📜httpStatus.ts
 ┃ ┃ ┗ 📜message.ts
 ┃ ┣ 📂controllers
 ┃ ┃ ┗ 📜users.controllers.ts
 ┃ ┣ 📂middlewares
 ┃ ┃ ┣ 📜error.middlewares.ts
 ┃ ┃ ┣ 📜file.middlewares.ts
 ┃ ┃ ┣ 📜users.middlewares.ts
 ┃ ┃ ┗ 📜validation.middlewares.ts
 ┃ ┣ 📂models
 ┃ ┃ ┣ 📂database
 ┃ ┃ ┃ ┣ 📜Blacklist.ts
 ┃ ┃ ┃ ┣ 📜Bookmark.ts
 ┃ ┃ ┃ ┣ 📜Follower.ts
 ┃ ┃ ┃ ┣ 📜Hashtag.ts
 ┃ ┃ ┃ ┣ 📜Like.ts
 ┃ ┃ ┃ ┣ 📜Media.ts
 ┃ ┃ ┃ ┣ 📜Tweet.ts
 ┃ ┃ ┃ ┗ 📜User.ts
 ┃ ┃ ┣ 📜Error.ts
 ┃ ┃ ┗ 📜Success.ts
 ┃ ┣ 📂routes
 ┃ ┃ ┗ 📜users.routes.ts
 ┃ ┣ 📂services
 ┃ ┃ ┣ 📜bookmarks.services.ts
 ┃ ┃ ┣ 📜database.services.ts
 ┃ ┃ ┣ 📜followers.services.ts
 ┃ ┃ ┣ 📜hashtags.services.ts
 ┃ ┃ ┣ 📜likes.services.ts
 ┃ ┃ ┣ 📜medias.services.ts
 ┃ ┃ ┣ 📜tweets.services.ts
 ┃ ┃ ┗ 📜users.services.ts
 ┃ ┣ 📂utils
 ┃ ┃ ┣ 📜crypto.ts
 ┃ ┃ ┣ 📜email.ts
 ┃ ┃ ┣ 📜file.ts
 ┃ ┃ ┣ 📜helpers.ts
 ┃ ┃ ┗ 📜jwt.ts
 ┃ ┣ 📜index.ts
 ┃ ┗ 📜type.d.ts
 ┣ 📜.editorconfig
 ┣ 📜.env
 ┣ 📜.eslintignore
 ┣ 📜.eslintrc
 ┣ 📜.gitignore
 ┣ 📜.prettierignore
 ┣ 📜.prettierrc
 ┣ 📜nodemon.json
 ┣ 📜package.json
 ┣ 📜tsconfig.json
 ┗ 📜yarn.lock

```

## Giải thích các thư mục:

- dist: Thư mục chứa các file build
- src: Thư mục chứa mã nguồn
- src/constants: Chứa các file chứa các hằng số
- src/middlewares: Chứa các file chứa các hàm xử lý middleware, như validate, check token, ...
- src/controllers: Chứa các file nhận request, gọi đến service để xử lý logic nghiệp vụ, trả về response
- src/services: Chứa các file chứa method gọi đến database để xử lý logic nghiệp vụ
- src/models: Chứa các file chứa các model
- src/routes: Chứa các file chứa các route
- src/utils: Chứa các file chứa các hàm tiện ích, như mã hóa, gửi email, ...
- Còn lại là những file config cho project như .eslintrc, .prettierrc, ... mình sẽ giới thiệu ở bên dưới

# Khởi tạo dự án

Đầu tiên chúng ta cần tạo folder để làm việc.

```bash
mkdir nodejs-typescript
cd nodejs-typescript
```

Tiếp theo, chúng ta sẽ setup dự án với package.json và thêm các dependencies cần thiết.

## Tạo dự án Node.js

Sử dụng -y khi chạy lệnh npm init khi tạo file package.json để không cần nhập các thông tin về project. Chúng ta có thể vào file package.json để chỉnh sửa sau.

```bash
npm init -y
```

## Thêm TypeScript như một dev dependency

Bước này chắc sẽ không bất ngờ lắm nhỉ, để sử dụng Typescript, chúng ta cần phải cài đặt nó trước.

```bash
npm install typescript --save-dev
```

Sau khi cài typescript, chúng ta có thể dùng TypeScript để biên dịch code bằng câu lệnh tsc (lưu ý là mình cài local nên muốn dùng tsc thì phải thông qua file package.json hoặc dùng npx tsc).

## Cài đặt kiểu dữ liệu TypeScript cho Node.js

```bash
npm install @types/node --save-dev
```

## Cài đặt các package config cần thiết còn lại

```bash
npm install eslint prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser ts-node tsc-alias tsconfig-paths rimraf nodemon --save-dev
```

### Note

- eslint: Linter (bộ kiểm tra lỗi) chính
- prettier: Code formatter chính
- eslint-config-prettier: Cấu hình ESLint để không bị xung đột với Prettier
- eslint-plugin-prettier: Dùng thêm một số rule prettier cho eslint
- @typescript-eslint/eslint-plugin: ESLint plugin cung cấp các rule cho Typescript
- @typescript-eslint/parser: Parser cho phép ESLint kiểm tra lỗi Typescript
- ts-node: Dùng để chạy TypeScript code trực tiếp mà không cần build
- tsc-alias: Xử lý alias khi build
- tsconfig-paths: Khi setting alias import trong dự án dùng ts-node thì chúng ta cần dùng tsconfig-paths để nó hiểu được paths và baseUrl trong file tsconfig.json
- rimraf: Dùng để xóa folder dist khi trước khi build
- nodemon: Dùng để tự động restart server khi có sự thay đổi trong code

# Cấu hình tsconfig.json

Tạo file tsconfig.json tại thư mục root, có thể tạo bằng lệnh touch tsconfig.json hoặc cứ tạo bằng tay, quen cái nào thì dùng cái đấy

Tiếp theo copy và paste cấu hình dưới đây vào file tsconfig.json của bạn

```json
{
  "compilerOptions": {
    "module": "NodeNext", // Quy định output module được sử dụng
    "moduleResolution": "NodeNext",
    "target": "ES2022", // Target output cho code
    "outDir": "dist", // Đường dẫn output cho thư mục build
    "esModuleInterop": true,
    "strict": true /* Enable all strict type-checking options. */,
    "skipLibCheck": true /* Skip type checking all .d.ts files. */,
    "baseUrl": ".", // Đường dẫn base cho các import
    "paths": {
      "~/*": ["src/*"] // Đường dẫn tương đối cho các import (alias)
    }
  },
  "ts-node": {
    "require": ["tsconfig-paths/register"]
  },
  "files": ["src/type.d.ts"], // Các file dùng để defined global type cho dự án
  "include": ["src/**/*"] // Đường dẫn include cho các file cần build
}
```

# Cấu hình file config cho ESLint

Tạo file .eslintrc tại thư mục root, copy và paste config dưới đây vào file .eslintrc của bạn

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint", "prettier"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "eslint-config-prettier",
    "prettier"
  ],
  "rules": {
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/no-unused-vars": "off",
    "prettier/prettier": [
      "warn",
      {
        "arrowParens": "always",
        "semi": false,
        "trailingComma": "none",
        "tabWidth": 2,
        "endOfLine": "auto",
        "useTabs": false,
        "singleQuote": true,
        "printWidth": 120,
        "jsxSingleQuote": true
      }
    ]
  }
}
```

Tiếp theo tạo file .eslintignore để ignore các file không cần kiểm tra lỗi

```json
node_modules/
dist/
```

# Cấu hình file config cho Prettier

Tạo file .prettierrc trong thư trong thư mục root với nội dung dưới đây

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

Tiếp theo Tạo file .prettierignore ở thư mục root

Mục đích là Prettier bỏ qua các file không cần thiết

```ignore
node_modules/
dist/
```

# Config editor để chuẩn hóa cấu hình editor

Tạo file .editorconfig ở thư mục root

Mục đích là cấu hình các config đồng bộ các editor với nhau nếu dự án có nhiều người tham gia.

Để VS Code hiểu được file này thì anh em cài Extension là EditorConfig for VS Code nhé

```Edittorconfig
[*]
indent_size = 2
indent_style = space
```

# Cấu hình file gitignore

Tạo file .gitignore ở thư mục root

Mục đích là cấu hình các file không cần đẩy lên git

```ignore
node_modules/
dist/
```

# Cấu hình file nodemon.json

Tạo file nodemon.json ở thư mục root

Mục đích là cấu hình nodemon để tự động restart server khi có sự thay đổi trong code

```json
{
  "watch": ["src"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "npx ts-node ./src/index.ts"
}
```

# Cấu hình file package.json

Mở file package.json lên, thêm đoạn script này vào

```json
  "scripts": {
    "dev": "npx nodemon",
    "build": "rimraf ./dist && tsc && tsc-alias",
    "start": "node dist/index.js",
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "prettier": "prettier --check .",
    "prettier:fix": "prettier --write ."
  }
```

# Tạo file type.d.ts

Tạo file type.d.ts trong thư mục src, tạm thời bây giờ các bạn để trống cũng được. Mục đích là để defined các global type cho dự án.

Các bạn mở file tsconfig.json lên sẽ thấy dòng mình add file này vào để cho typescript nó nhận diện
