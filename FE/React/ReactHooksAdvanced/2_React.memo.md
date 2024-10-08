# React.memo

Chúng ta dùng React.memo khi không muốn component bị re-render mỗi khi component cha re-render

> Các tác nhân làm component re-render: cập nhật state, cập nhật prop, component cha re-render

React.memo là một HOC, vậy nên chỉ cần bao bọc component là được

```jsx
const newComponent = React.memo(Component);
```

React.memo chỉ tác động đến prop, không ảnh hưởng đến state

Cơ chế memo là cơ chế dùng bộ nhớ (RAM) để lưu trữ, vì thế khi dùng những thứ liên quan đến memo nghĩa là chúng ta đang đánh đổi giữa tốn nhiều bộ nhớ hơn để tăng tốc performance.

Vậy nên đừng lạm dụng quá nhé!
