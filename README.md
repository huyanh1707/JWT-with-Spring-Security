# Spring Security with JWT vs Swagger

## Spring Security

- WebSecurityConfigurerAdapter: là mấu chốt của việc triển khai bảo mật của Spring. Nó cung cấp các cấu hình
  HTTPSecurity để cấu hình cors, csrf, quản lý phiên, các luật cho tài nguyên được bảo vệ.
- UserDetailsService: là interface có các phương thức để cập nhật User bằng username và trả lại một đối tượng
  UserDetails mà Spring Security có thể sử dụng cho việc xác thực và validation.
- UserDetails chứa các thông tin cần thiết (như: username, password, authorities) để xây dựng một đối tượng bảo mật.
- UsernamePasswordAuthenticationToken lấy username, password từ việc đăng nhập và AuthenticationManager sử dụng chúng để
  xác thực một tài khoản đăng nhập
- AuthenticationManager có DaoAuthenticationProvider (với sự trợ giúp của UserDetailsService & PasswordEncoder) để xác
  thực đối tượng UsernamePasswordAuthenticationToken. Nếu thành công, AuthenticationManager trả về một đối tượng Xác
  thực được điền đầy đủ (bao gồm cả các authorities được cấp
- OncePerRequestFilter thực hiện một lần thực thi duy nhất cho mỗi yêu cầu tới API. Nó cung cấp một phương
  thức doFilterInternal () triển khai phân tích cú pháp và xác thực JWT, tải chi tiết Người dùng (sử dụng UserDetailsService), kiểm tra Authorizaion (sử dụng UsernamePasswordAuthenticationToken).
- AuthenticationEntryPoint sẽ bắt các lỗi xác thực.

## Class Description

## `JwtUtil`

The `JwtUtil` is responsible for performing JWT operators like creation and validation of the token.

Lớp `JwtUtil` chịu trách nhiệm khởi tạo JWT như tạo và xác thực token

## `AuthTokenFilter`

The `AuthTokenFilter` extends the Spring Web Filter `OncePerRequestFilter` class. For any incoming request, this Filter
class get executed. It checks if request has a valid JWT token then it sets the Authentication in the context, to
specify that the current user is authenticated.

Lớp `AuthTokenFilter` được kế thừa từ lớp Filter của Spring là lớp `OncePerRequestFilter`. Khi bất kì request đi qua,
lớp Filter này sẽ được thực thi. Nó sẽ kiểm tra nếu request có một JWT hợp lệ thì nó sẽ cài đặt Authentication vào trong
ngữ cảnh, để chỉ định rằng người dùng hiện tại đã được xác thực.

## `AuthEntryPoint`

The `AuthEntryPoint` extends Spring’s `AuthenticationEntryPoint` class and overrides its method commence. It rejects
every unauthenticated request and sends error code 401.

Lớp `AuthEntryPoint` được kế thừa từ lớp `AuthenticationEntryPoint` của Spring và overrides lại class khởi tạo cảu nó.
Nó từ chối mọi yêu cầu không xác thực và gửi lại mã lỗi 401.

## `WebSecurityConfig`

The `WebSecurityConfig` class extends the `WebSecurityConfigurerAdapter` which is a convenience class that allows
customization to both WebSecurity and HttpSecurity.

Lớp `WebSecurityConfig` kế thừa từ lớp `WebSecurityConfigurerAdapter` là một lớp cho phép custom cả WebSecurity và
HttpSecurity.


