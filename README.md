<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Art Store - COD Available</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #fff;
      padding: 20px;
      margin: 0;
    }
    .container {
      max-width: 800px;
      margin: auto;
      text-align: center;
    }
    .banner {
      background-color: #ffcc00;
      color: #000;
      padding: 15px;
      font-size: 1.2em;
      font-weight: bold;
      border-radius: 8px;
      margin-bottom: 20px;
    }
    #countdown {
      font-size: 1em;
      color: #d32f2f;
      margin-top: 5px;
    }
    h1 {
      font-size: 2.2em;
      margin-bottom: 5px;
    }
    h2 {
      font-size: 1.4em;
      color: green;
      margin-bottom: 20px;
    }
    img {
      max-width: 100%;
      border-radius: 10px;
      border: 4px solid #8B4513;
    }
    .product {
      margin-top: 20px;
    }
    .price-box {
      font-size: 1.1em;
      margin-top: 10px;
    }
    .original-price {
      text-decoration: line-through;
      color: #888;
    }
    .discounted-price {
      color: #e53935;
      font-weight: bold;
    }
    form {
      margin-top: 30px;
      text-align: left;
      padding: 20px;
      border-radius: 10px;
      border: 1px solid #ccc;
      background-color: #f5f5f5;
    }
    label {
      display: block;
      margin-top: 10px;
      font-weight: bold;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      margin-bottom: 15px;
      border-radius: 5px;
      border: 1px solid #aaa;
    }
    button {
      width: 100%;
      background-color: #00695c;
      color: white;
      padding: 12px;
      font-size: 1em;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #004d40;
    }
    @media screen and (max-width: 600px) {
      .banner {
        font-size: 1em;
        padding: 10px;
      }
      h1 {
        font-size: 1.8em;
      }
      h2 {
        font-size: 1.2em;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="banner">
      🎓 College Students Get <strong>40% OFF</strong>! Show your student ID at delivery.
      <br>🔥 Offer ends on <strong>20 May 2025</strong>!
      <div id="countdown"></div>
    </div>

    <h1>Art Store</h1>
    <h2>Cash on Delivery Available</h2>

    <div class="product">
      <img src="A_webpage_screenshot_for_an_online_store_named_&quot;Ar.png" alt="AI Art Image">
      <h3>AI Art Image</h3>
      <p style="max-width: 600px; margin: 0 auto; font-size: 1em; color: #444;">
        This exclusive AI-generated artwork blends creativity and technology to create a one-of-a-kind masterpiece. Perfect for modern homes, workspaces, or gifting, this digital art captures emotion, imagination, and innovation in every pixel. Own a piece of the future today!
      </p>
      <div class="price-box">
        <span class="original-price">₹833</span> &nbsp;
        <span class="discounted-price">Now Only ₹500</span>
      </div>
    </div>

    <form method="POST" action="index.php" enctype="multipart/form-data">
      <h3>Place Your Order</h3>
      <label for="name">Full Name:</label>
      <input type="text" id="name" name="name" required>

      <label for="address">Delivery Address:</label>
      <input type="text" id="address" name="address" required>

      <label for="email">Email Address:</label>
      <input type="email" id="email" name="email" required>

      <label for="mobile">Mobile Number:</label>
      <input type="text" id="mobile" name="mobile" required>

      <label for="product">Choose Product:</label>
      <select id="product" name="product">
        <option value="AI Art Image">AI Art Image - ₹500</option>
      </select>

      <label for="studentID">Upload Student ID (for discount verification):</label>
      <input type="file" id="studentID" name="studentID" accept=".jpg,.jpeg,.png,.pdf" required>

      <p><strong>Payment Method:</strong> Cash on Delivery</p>

      <button type="submit">Place Order</button>
    </form>
  </div>

  <script>
    // Countdown Timer to 20 May 2025
    const endDate = new Date("May 20, 2025 23:59:59").getTime();
    const countdown = document.getElementById("countdown");

    const updateCountdown = setInterval(() => {
      const now = new Date().getTime();
      const distance = endDate - now;

      if (distance < 0) {
        clearInterval(updateCountdown);
        countdown.innerHTML = "🎉 Offer has ended!";
        return;
      }

      const days = Math.floor(distance / (1000 * 60 * 60 * 24));
      const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((distance % (1000 * 60)) / 1000);

      countdown.innerHTML = `⏳ ${days}d ${hours}h ${minutes}m ${seconds}s left!`;
    }, 1000);
  </script>

  <?php
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $name = $_POST['name'];
      $address = $_POST['address'];
      $email = $_POST['email'];
      $mobile = $_POST['mobile'];
      $product = $_POST['product'];

      // Save uploaded file
      $target_dir = "uploads/";
      $target_file = $target_dir . basename($_FILES["studentID"]["name"]);
      move_uploaded_file($_FILES["studentID"]["tmp_name"], $target_file);

      // Send email with the order details
      $to = "anime24453@gmail.com";
      $subject = "New Order Received";
      $message = "
      <html>
      <head>
          <title>New Order</title>
      </head>
      <body>
          <h2>Order Details</h2>
          <p><strong>Name:</strong> $name</p>
          <p><strong>Address:</strong> $address</p>
          <p><strong>Email:</strong> $email</p>
          <p><strong>Mobile:</strong> $mobile</p>
          <p><strong>Product Ordered:</strong> $product</p>
          <p><strong>Student ID Uploaded:</strong> <a href='$target_file'>View File</a></p>
      </body>
      </html>";

      // Set content-type header for HTML email
      $headers = "MIME-Version: 1.0" . "\r\n";
      $headers .= "Content-type:text/html;charset=UTF-8" . "\r\n";
      $headers .= "From: <no-reply@artstore.com>" . "\r\n";

      if (mail($to, $subject, $message, $headers)) {
          echo "<script>alert('Order placed successfully!');</script>";
      } else {
          echo "<script>alert('Failed to send the order details.');</script>";
      }
  }
  ?>
</body>
</html>
