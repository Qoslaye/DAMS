<?php

/**
 * Doctor Appointment Management System
 * 
 * This is a simple Doctor Appointment Management System built using PHP and MySQL. 
 * The system allows doctors to manage appointments and provides a form for patients 
 * to submit their details and preferred appointment time.
 */

// Database configuration
$host = 'localhost';
$db = 'database_name';
$user = 'username';
$password = 'password';

try {
    $conn = new PDO("mysql:host=$host;dbname=$db", $user, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    die("Connection failed: " . $e->getMessage());
}

// Patient Appointment Form Handling
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $name = $_POST['name'];
    $contact = $_POST['contact'];
    $appointment_date = $_POST['appointment_date'];

    $stmt = $conn->prepare("INSERT INTO appointments (name, contact, appointment_date) VALUES (:name, :contact, :appointment_date)");
    $stmt->bindParam(':name', $name);
    $stmt->bindParam(':contact', $contact);
    $stmt->bindParam(':appointment_date', $appointment_date);

    if ($stmt->execute()) {
        echo "Appointment booked successfully.";
    } else {
        echo "Failed to book appointment.";
    }
}

?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Doctor Appointment Management System</title>
</head>
<body>
    <h1>Doctor Appointment Management System</h1>

    <!-- Patient Appointment Form -->
    <form method="POST" action="">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required><br>

        <label for="contact">Contact:</label>
        <input type="text" id="contact" name="contact" required><br>

        <label for="appointment_date">Appointment Date:</label>
        <input type="date" id="appointment_date" name="appointment_date" required><br>

        <button type="submit">Book Appointment</button>
    </form>

    <!-- Doctor Section Placeholder -->
    <h2>Doctor Section</h2>
    <p>Login to manage appointments.</p>

</body>
</html>

