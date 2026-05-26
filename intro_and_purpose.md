# Giới Thiệu Về Giao Thức Trao Đổi Khóa Diffie-Hellman

## 1. Diffie-Hellman là gì?
Hãy tưởng tượng bạn và một người bạn muốn trò chuyện bí mật bằng một chiếc hộp có khóa. Nhưng hai người ở rất xa nhau và chưa từng gặp mặt để đưa nhau chìa khóa. Làm thế nào để cả hai có được một chiếc chìa khóa giống hệt nhau mà không cần gửi nó qua bưu điện (nơi thư có thể bị bóc trộm)?

**Diffie-Hellman (DH)** là phương thức giải quyết vấn đề này. 

Được phát minh bởi Whitfield Diffie và Martin Hellman vào năm 1976, đây là một giao thức mã hóa cho phép hai bên **tự thiết lập một khóa bí mật chung** (shared secret key) thông qua một kênh truyền thông không an toàn (như Internet công cộng) mà không cần phải gửi chính chiếc khóa đó cho nhau.

---

## 2. Mục đích của Diffie-Hellman
Trong thế giới mã hóa, chúng ta có hai loại chính:
*   **Mã hóa đối xứng (Symmetric Encryption):** Rất nhanh và an toàn, nhưng đòi hỏi hai bên phải có chung một chiếc khóa từ trước.
*   **Mã hóa bất đối xứng (Asymmetric Encryption):** Cho phép trao đổi thông tin an toàn không cần gặp trước, nhưng tốc độ xử lý lại rất chậm.

**Mục đích của Diffie-Hellman:** 
Đóng vai trò là "cầu nối" hoàn hảo. Nó tận dụng tính linh hoạt của mã hóa bất đối xứng để giúp hai bên tạo ra một chiếc khóa chung. Sau khi đã có khóa chung này, họ sẽ chuyển sang dùng mã hóa đối xứng để truyền dữ liệu cực nhanh.

> **Tóm lại:** Diffie-Hellman không dùng để mã hóa trực tiếp nội dung tin nhắn, mục đích duy nhất của nó là **thống nhất một chiếc khóa chung** giữa hai bên một cách an toàn.

---

## 3. Ý tưởng cốt lõi: Ví dụ về "Pha màu sơn"
Để hiểu cách Diffie-Hellman hoạt động trước khi đi vào các con số, hãy xem ví dụ kinh điển về việc pha màu sơn dưới đây:

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
        <span style="font-family: 'Courier New', monospace; font-size: 15px; font-weight: bold; color: #0284c7;">A = g<sup>a</sup> mod p</span>
      </td>
      <td style="padding: 15px; text-align: center; vertical-align: middle; background-color: #ffffff; border-left: 1px solid #f1f5f9; border-right: 1px solid #f1f5f9;">
        &nbsp;
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: middle;">
        Tính khóa công khai B:<br>
        <span style="font-family: 'Courier New', monospace; font-size: 15px; font-weight: bold; color: #0284c7;">B = g<sup>b</sup> mod p</span>
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
          K = B<sup>a</sup> mod p<br>
          K = (g<sup>b</sup>)<sup>a</sup> mod p<br>
          K = <strong>g<sup>ab</sup> mod p</strong>
        </span>
      </td>
      <td style="padding: 15px; text-align: center; vertical-align: middle; background-color: #f8fafc; border-left: 1px solid #f1f5f9; border-right: 1px solid #f1f5f9;">
        &nbsp;
      </td>
      <td style="padding: 15px; text-align: right; vertical-align: top; line-height: 1.6;">
        <strong>Tính khóa chung K:</strong><br>
        <span style="font-family: 'Courier New', monospace; font-size: 14px; color: #334155;">
          K = A<sup>b</sup> mod p<br>
          K = (g<sup>a</sup>)<sup>b</sup> mod p<br>
          K = <strong>g<sup>ab</sup> mod p</strong>
        </span>
      </td>
    </tr>
    <!-- Bước cuối: Kết quả -->
    <tr style="background-color: #f0fdf4;">
      <td colspan="3" style="padding: 20px; text-align: center; vertical-align: middle; border-top: 2px solid #bbf7d0;">
        <div style="font-size: 11px; text-transform: uppercase; letter-spacing: 1.5px; color: #166534; font-weight: bold; margin-bottom: 4px;">Kết quả thiết lập thành công</div>
        <div style="font-size: 18px; font-weight: bold; color: #14532d; font-family: 'Courier New', monospace;">
          [ KHÓA CHUNG BÍ MẬT K = g<sup>ab</sup> mod p ]
        </div>
      </td>
    </tr>
  </tbody>
</table>

---

## 4. Giải thích Toán học một cách dễ hiểu
Phép toán "pha màu" ở trên trong thế giới số được thực hiện thông qua **Phép chia lấy dư (Modulo)** và **Số mũ**.

### Phép toán Modulo - "Chiếc đồng hồ một chiều"
Trong toán học, $A \pmod p$ nghĩa là lấy $A$ chia cho $p$ và giữ lại phần dư. 
*   *Ví dụ:* $17 \pmod{12} = 5$ (giống như 17 giờ chiều trên mặt đồng hồ 12 số thực chất là 5 giờ).
*   **Tính chất một chiều:** Nếu biết $3^x \pmod{17} = 12$, việc tìm ra $x$ là cực kỳ khó khăn nếu các số lớn lên tới hàng trăm chữ số. Đây gọi là bài toán **Lôgarit rời rạc** – nền tảng bảo mật của Diffie-Hellman.

### Các bước tạo khóa bằng công thức
Hãy xem các con số được "pha" như thế nào:

#### Bước 1: Thống nhất thông số công khai (Màu sơn chung)
Alice và Bob đồng ý sử dụng hai số công khai:
*   $p$: Một số nguyên tố rất lớn.
*   $g$: Một số nguyên nhỏ (gọi là phần tử sinh).
*(Ai cũng có thể biết hai số này).*

#### Bước 2: Chọn khóa bí mật riêng (Màu sơn riêng)
*   Alice chọn một số ngẫu nhiên $a$ (giữ bí mật cho riêng mình).
*   Bob chọn một số ngẫu nhiên $b$ (giữ bí mật cho riêng mình).

#### Bước 3: Tính toán và trao đổi (Gửi màu đã pha)
*   Alice tính khóa công khai của mình: 
    $$A = g^a \pmod p$$
    Sau đó gửi $A$ cho Bob.
*   Bob tính khóa công khai của mình: 
    $$B = g^b \pmod p$$
    Sau đó gửi $B$ cho Alice.

#### Bước 4: Tạo ra khóa chung cuối cùng
Bây giờ, phép thuật toán học xảy ra:
*   Alice nhận được $B$ từ Bob, cô ấy lũy thừa với số bí mật $a$ của mình:
    $$K_{Alice} = B^a \pmod p = (g^b)^a \pmod p = g^{ab} \pmod p$$
*   Bob nhận được $A$ từ Alice, anh ấy lũy thừa với số bí mật $b$ của mình:
    $$K_{Bob} = A^b \pmod p = (g^a)^b \pmod p = g^{ab} \pmod p$$

Vì $(g^a)^b$ bằng $(g^b)^a$ (đều bằng $g^{ab}$), nên cuối cùng:
$$K_{Alice} = K_{Bob} = K$$

Hai bên đã có chung một số $K$ để làm khóa mã hóa mà không một ai ngoài giao lộ biết được khóa này.

---

## 5. Kết luận
Diffie-Hellman là một giải pháp đơn giản nhưng tinh tế cho bài toán phân phối khóa. Bằng cách sử dụng các phép toán số mũ và chia lấy dư một chiều, nó biến việc chia sẻ bí mật qua môi trường không an toàn trở nên khả thi. Nó là nền tảng cho hầu hết các kết nối an toàn trên Internet hiện nay mà chúng ta dùng hàng ngày, như HTTPS hay giao thức bảo mật SSH.
