# Tìm Hiểu Về Giao Thức Trao Đổi Khóa Diffie-Hellman

## 1. Đặt vấn đề và Khái niệm

Giả sử có 2 người bạn muốn trò chuyện bí mật bằng một chiếc hộp có khóa. Nhưng hai người ở rất xa nhau và chưa từng gặp mặt để đưa nhau chìa khóa. Làm thế nào để cả hai có được một chiếc chìa khóa giống hệt nhau mà không cần gửi nó công khai qua bưu điện?

Giao thức **Diffie-Hellman** chính là phương thức giải quyết vấn đề này.

Được phát minh bởi **Whitfield Diffie** và **Martin Hellman** vào năm 1976, đây là một giao thức mã hóa cho phép hai bên tự thiết lập một khóa bí mật chung thông qua một kênh truyền thông không an toàn (như Internet công cộng) mà không cần phải gửi chính chiếc khóa đó cho nhau.

---

## 2. Mục đích của giao thức
Trong mật mã học, các thuật toán thường được chia làm hai loại:
* **Mã hóa đối xứng:** Tốc độ xử lý nhanh và an toàn, nhưng bắt buộc hai bên phải sở hữu chung một khóa từ trước.
* **Mã hóa bất đối xứng:** Cho phép giao tiếp an toàn mà không cần gặp nhau để chia sẻ khóa, nhưng tốc độ xử lý chậm và tốn tài nguyên.

Diffie-Hellman ra đời để kết hợp ưu điểm của cả hai phương pháp trên. Giao thức này đóng vai trò thiết lập một khóa chung ban đầu dựa trên cơ chế bất đối xứng. Khi đã có được khóa chung này, hai bên sẽ chuyển sang dùng mã hóa đối xứng để truyền dữ liệu thực tế nhằm đạt tốc độ tối đa.

Giao thức này không dùng để mã hóa trực tiếp nội dung tin nhắn, mà mục đích duy nhất của nó là **thống nhất một chiếc khóa chung** giữa hai bên một cách an toàn.

---

## 3. Quy trình thiết lập khóa
Quy trình tính toán và trao đổi thông tin giữa Alice và Bob được thực hiện trực tiếp qua các bước dưới đây:

<table style="width: 100%; border-collapse: collapse; font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, Arial, sans-serif; font-size: 14px; margin: 25px 0; background-color: #ffffff; box-shadow: 0 4px 12px rgba(0,0,0,0.08); border-radius: 8px; overflow: hidden; border: 1px solid #e2e8f0;">
  <thead>
    <tr style="background-color: #1e293b; color: #f8fafc;">
      <th style="width: 38%; padding: 15px; text-align: left; border-bottom: 2px solid #0f172a;">Phía Alice (Bảo mật)</th>
      <th style="width: 24%; padding: 15px; text-align: center; border-bottom: 2px solid #0f172a; background-color: #991b1b;">Kênh truyền công khai<br><span style="font-size: 11px; font-weight: normal; opacity: 0.9;">(Bị nghe lén)</span></th>
      <th style="width: 38%; padding: 15px; text-align: right; border-bottom: 2px solid #0f172a;">Phía Bob (Bảo mật)</th>
    </tr>
  </thead>
  <tbody>
    <!-- Bước 1: Thống nhất tham số -->
    <tr style="border-bottom: 1px solid #f1f5f9;">
      <td style="padding: 15px; vertical-align: middle;">
        <strong>Thống nhất tham số chung:</strong><br>
        <span style="color: #64748b;">Số nguyên tố p và phần tử sinh g</span>
      </td>
      <td style="padding: 15px; text-align: center; vertical-align: middle; background-color: #fffbeb; font-weight: bold; color: #b45309; border-left: 1px solid #fef3c7; border-right: 1px solid #fef3c7;">
        $g$, $p$ công khai
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: middle;">
        &nbsp;
      </td>
    </tr>
    <!-- Bước 2: Chọn khóa riêng -->
    <tr style="border-bottom: 1px solid #f1f5f9; background-color: #f8fafc;">
      <td style="padding: 15px; vertical-align: middle;">
        Chọn khóa riêng ngẫu nhiên:<br>
        <span style="color: #0f172a; font-weight: bold; font-family: 'Courier New', monospace; font-size: 16px;">a</span>
      </td>
      <td style="padding: 15px; text-align: center; vertical-align: middle; background-color: #f8fafc; border-left: 1px solid #f1f5f9; border-right: 1px solid #f1f5f9;">
        &nbsp;
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: middle;">
        Chọn khóa riêng ngẫu nhiên:<br>
        <span style="color: #0f172a; font-weight: bold; font-family: 'Courier New', monospace; font-size: 16px;">b</span>
      </td>
    </tr>
    <!-- Bước 3: Tính khóa công khai -->
    <tr style="border-bottom: 1px solid #f1f5f9;">
      <td style="padding: 15px; vertical-align: middle;">
        Tính khóa công khai A:<br>
        <span style="font-family: 'Courier New', monospace; font-size: 15px; font-weight: bold; color: #0284c7;">A = g<sup>a</sup> (mod p)</span>
      </td>
      <td style="padding: 15px; text-align: center; vertical-align: middle; background-color: #ffffff; border-left: 1px solid #f1f5f9; border-right: 1px solid #f1f5f9;">
        &nbsp;
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: middle;">
        Tính khóa công khai B:<br>
        <span style="font-family: 'Courier New', monospace; font-size: 15px; font-weight: bold; color: #0284c7;">B = g<sup>b</sup> (mod p)</span>
      </td>
    </tr>
    <!-- Bước 4: Gửi A -->
    <tr style="border-bottom: 1px solid #f1f5f9; background-color: #f8fafc;">
      <td style="padding: 15px; vertical-align: middle;">
        &nbsp;
      </td>
      <td style="padding: 12px 15px; text-align: center; vertical-align: middle; background-color: #fffbeb; border-left: 1px solid #fef3c7; border-right: 1px solid #fef3c7;">
        <div style="font-size: 11px; color: #78350f; font-weight: 500; margin-bottom: 2px;">Gửi khóa công khai A</div>
        <div style="font-size: 20px; color: #0284c7; line-height: 1; margin-bottom: 2px;">➔</div>
        <div style="font-family: 'Courier New', monospace; font-weight: bold; color: #0f172a; font-size: 15px;">A</div>
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: middle;">
        Nhận được khóa <span style="font-family: 'Courier New', monospace; font-weight: bold; color: #0284c7;">A</span> từ Alice
      </td>
    </tr>
    <!-- Bước 5: Gửi B -->
    <tr style="border-bottom: 1px solid #f1f5f9;">
      <td style="padding: 15px; vertical-align: middle;">
        Nhận được khóa <span style="font-family: 'Courier New', monospace; font-weight: bold; color: #0284c7;">B</span> từ Bob
      </td>
      <td style="padding: 12px 15px; text-align: center; vertical-align: middle; background-color: #fffbeb; border-left: 1px solid #fef3c7; border-right: 1px solid #fef3c7;">
        <div style="font-size: 11px; color: #78350f; font-weight: 500; margin-bottom: 2px;">Gửi khóa công khai B</div>
        <div style="font-size: 20px; color: #0284c7; line-height: 1; margin-bottom: 2px;">◀</div>
        <div style="font-family: 'Courier New', monospace; font-weight: bold; color: #0f172a; font-size: 15px;">B</div>
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: middle;">
        &nbsp;
      </td>
    </tr>
    <!-- Bước 6: Tính khóa chung -->
    <tr style="border-bottom: 2px solid #e2e8f0; background-color: #f8fafc;">
      <td style="padding: 15px; vertical-align: top; line-height: 1.6;">
        <strong>Tính khóa chung K:</strong><br>
        <span style="font-family: 'Courier New', monospace; font-size: 14px; color: #334155;">
          K = B<sup>a</sup> (mod p)<br>
          K = (g<sup>b</sup>)<sup>a</sup> (mod p)<br>
          K = <strong>g<sup>ab</sup> (mod p)</strong>
        </span>
      </td>
      <td style="padding: 15px; text-align: center; vertical-align: middle; background-color: #f8fafc; border-left: 1px solid #f1f5f9; border-right: 1px solid #f1f5f9;">
        &nbsp;
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: top; line-height: 1.6;">
        <strong>Tính khóa chung K:</strong><br>
        <span style="font-family: 'Courier New', monospace; font-size: 14px; color: #334155;">
          K = A<sup>b</sup> (mod p)<br>
          K = (g<sup>a</sup>)<sup>b</sup> (mod p)<br>
          K = <strong>g<sup>ab</sup> (mod p)</strong>
        </span>
      </td>
    </tr>
    <!-- Bước cuối: Kết quả -->
    <tr style="background-color: #f0fdf4;">
      <td colspan="3" style="padding: 20px; text-align: center; vertical-align: middle; border-top: 2px solid #bbf7d0;">
        <div style="font-size: 11px; text-transform: uppercase; letter-spacing: 1.5px; color: #166534; font-weight: bold; margin-bottom: 4px;">Kết quả thiết lập thành công</div>
        <div style="font-size: 18px; font-weight: bold; color: #14532d; font-family: 'Courier New', monospace;">
          [ KHÓA CHUNG BÍ MẬT K = g<sup>ab</sup> (mod p) ]
        </div>
      </td>
    </tr>
  </tbody>
</table>

---

## 4. Cơ sở toán học của giao thức

Tính bảo mật của Diffie-Hellman dựa trên hai yếu tố toán học cốt lõi dưới đây.

### 4.1. Phép toán Modulo và tính chất hàm một chiều

Phép toán $A \pmod p$ có thể được hiểu đơn giản là phép chia lấy phần dư.

Trong mật mã học, phép toán này được sử dụng như một **hàm một chiều**:
* **Tính toán theo chiều xuôi:** Nếu biết số mũ $a = 5$, cơ số $g = 3$, và số chia $p = 17$, máy tính chỉ mất ít thời gian để tính ra $A = 3^5 \pmod{17} = 5$.
* **Tính toán theo chiều ngược lại:** Nếu chỉ biết kết quả $A = 5$, cơ số $g = 3$, và số chia $p = 17$, để tìm lại số mũ $a$ ban đầu thỏa mãn phương trình $3^a \pmod{17} = 5$, chúng ta bắt buộc phải thử sai từng trường hợp.

Khi áp dụng vào thực tế, số nguyên tố $p$ được chọn là một số cực kỳ lớn (thường dài hơn 600 chữ số). Với kích thước này, việc tìm ngược lại khóa riêng $a$ từ khóa công khai $A$ là bất khả thi đối với các máy tính hiện nay. Trong toán học, đây được gọi là **Bài toán Lôgarit rời rạc (Discrete Logarithm Problem)**.

### 4.2. Tính chất giao hoán của phép lũy thừa

Yếu tố giúp Alice và Bob tính toán ra cùng một khóa chung $K$ nằm ở tính chất giao hoán cơ bản của lũy thừa:
$$(g^a)^b = (g^b)^a = g^{ab}$$

Dựa vào sơ đồ trao đổi ở phần 3:
* Alice nhận khóa công khai $B = g^b \pmod p$ từ Bob. Sau đó, Alice tự tính khóa chung bằng cách nâng $B$ lên lũy thừa khóa riêng $a$ của mình:
  $$K = B^a \pmod p = (g^b)^a \pmod p = g^{ab} \pmod p$$
* Bob nhận khóa công khai $A = g^a \pmod p$ từ Alice. Bob tính khóa chung bằng cách nâng $A$ lên lũy thừa khóa riêng $b$ của mình:
  $$K = A^b \pmod p = (g^a)^b \pmod p = g^{ab} \pmod p$$

Cả hai người thực hiện các phép tính hoàn toàn độc lập với những mảnh thông tin khác nhau, nhưng về mặt toán học, kết quả cuối cùng thu được đều là $g^{ab} \pmod p$. 

Trong khi đó, kẻ nghe lén trên đường truyền chỉ thu thập được các thông tin công khai $\{g, p, A, B\}$. Nếu không có khóa riêng $a$ của Alice hoặc $b$ của Bob, kẻ tấn công không thể nào tính ra được khóa chung $K$.

---

## 5. Đánh giá và Ứng dụng
Diffie-Hellman là một giải pháp tối ưu cho bài toán phân phối khóa nhờ tính đơn giản nhưng chặt chẽ về mặt toán học. Bằng cách biến việc trao đổi thông tin thành các phép tính lũy thừa một chiều, giao thức này giúp việc chia sẻ bí mật trên môi trường Internet trở nên an toàn.

Ngày nay, Diffie-Hellman là thành phần nền tảng được tích hợp trong hầu hết các giao thức bảo mật mạng phổ biến như HTTPS (thông qua SSL/TLS), SSH (truy cập máy chủ từ xa), và các kết nối VPN.
