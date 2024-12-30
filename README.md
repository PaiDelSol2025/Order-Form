<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pie Order Form</title>
</head>
<body>
    <h1>Pie Order Form</h1>
    <form id="orderForm">
        <label for="name">Name:</label><br>
        <input type="text" id="name" name="name" required><br><br>

        <label for="email">Email:</label><br>
        <input type="email" id="email" name="email" required><br><br>

        <label for="phone">Phone Number:</label><br>
        <input type="tel" id="phone" name="phone" required><br><br>

        <label for="pie">Choose Your Pie:</label><br>
        <select id="pie" name="pie" required>
            <option value="Apple Pie">Apple Pie</option>
            <option value="Strawberry Pie">Strawberry Pie</option>
            <option value="Pecan Pie">Pecan Pie</option>
            <option value="Pumpkin Pie">Pumpkin Pie</option>
            <option value="Pumpkin Pie with Pecan Nut Crust">Pumpkin Pie with Pecan Nut Crust</option>
        </select><br><br>

        <label for="quantity">Quantity:</label><br>
        <input type="number" id="quantity" name="quantity" min="1" required><br><br>

        <label for="notes">Additional Notes:</label><br>
        <textarea id="notes" name="notes" rows="4"></textarea><br><br>

        <button type="submit">Place Order</button>
    </form>

    <script>
        document.getElementById('orderForm').addEventListener('submit', function(event) {
            event.preventDefault(); // Prevent default form submission

            // Collect form data
            const formData = new FormData(event.target);
            const data = {
                name: formData.get('name'),
                email: formData.get('email'),
                phone: formData.get('phone'),
                pie: formData.get('pie'),
                quantity: formData.get('quantity'),
                notes: formData.get('notes')
            };

            // Send order details to your email via a backend service
            fetch('https://your-backend-endpoint.com/send-order', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(data)
            })
            .then(response => {
                if (response.ok) {
                    alert('Your order has been placed!');
                    event.target.reset();
                } else {
                    alert('There was an issue placing your order. Please try again.');
                }
            })
            .catch(error => {
                console.error('Error:', error);
                alert('There was an error placing your order. Please try again later.');
            });
        });
    </script>
</body>
</html>
