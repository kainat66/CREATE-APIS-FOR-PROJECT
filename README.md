<?php
header("Content-Type: application/json");

$conn = mysqli_connect("localhost", "your_username", "your_password", "event_management");

if (!$conn) {
    die(json_encode(["error" => "Connection failed: " . mysqli_connect_error()]));
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $data = json_decode(file_get_contents("php://input"), true);

    $title = $data["title"];
    $description = $data["description"];
    $date_time = $data["date_time"];

    $query = "INSERT INTO events (title, description, date_time) VALUES ('$title', '$description', '$date_time')";

    if (mysqli_query($conn, $query)) {
        echo json_encode(["message" => "Event created successfully"]);
    } else {
        echo json_encode(["error" => "Error: " . $query . "<br>" . mysqli_error($conn)]);
    }
} else {
    echo json_encode(["error" => "Invalid request method"]);
}

mysqli_close($conn);
?>
<?php
header("Content-Type: application/json");

$conn = mysqli_connect("localhost", "your_username", "your_password", "event_management");

if (!$conn) {
    die(json_encode(["error" => "Connection failed: " . mysqli_connect_error()]));
}

$query = "SELECT * FROM events ORDER BY date_time";
$result = mysqli_query($conn, $query);

$events = [];
while ($row = mysqli_fetch_assoc($result)) {
    $events[] = $row;
}

echo json_encode($events);

mysqli_close($conn);
?>
<?php
header("Content-Type: application/json");

$conn = mysqli_connect("localhost", "your_username", "your_password", "event_management");

if (!$conn) {
    die(json_encode(["error" => "Connection failed: " . mysqli_connect_error()]));
}

$query = "SELECT * FROM events ORDER BY date_time";
$result = mysqli_query($conn, $query);

$events = [];
while ($row = mysqli_fetch_assoc($result)) {
    $events[] = $row;
}

echo json_encode($events);

mysqli_close($conn);
?>
Update Event (PUT Request):

update_event.php

php
Copy code
<?php
header("Content-Type: application/json");

$conn = mysqli_connect("localhost", "your_username", "your_password", "event_management");

if (!$conn) {
    die(json_encode(["error" => "Connection failed: " . mysqli_connect_error()]));
}

if ($_SERVER["REQUEST_METHOD"] == "PUT") {
    $data = json_decode(file_get_contents("php://input"), true);

    $event_id = $data["id"];
    $title = $data["title"];
    $description = $data["description"];
    $date_time = $data["date_time"];

    $query = "UPDATE events SET title='$title', description='$description', date_time='$date_time' WHERE id=$event_id";

    if (mysqli_query($conn, $query)) {
        echo json_encode(["message" => "Event updated successfully"]);
    } else {
        echo json_encode(["error" => "Error: " . $query . "<br>" . mysqli_error($conn)]);
    }
} else {
    echo json_encode(["error" => "Invalid request method"]);
}

mysqli_close($conn);
?>
<?php
header("Content-Type: application/json");

$conn = mysqli_connect("localhost", "your_username", "your_password", "event_management");

if (!$conn) {
    die(json_encode(["error" => "Connection failed: " . mysqli_connect_error()]));
}

if ($_SERVER["REQUEST_METHOD"] == "DELETE") {
    $data = json_decode(file_get_contents("php://input"), true);

    $event_id = $data["id"];

    $query = "DELETE FROM events WHERE id=$event_id";

    if (mysqli_query($conn, $query)) {
        echo json_encode(["message" => "Event deleted successfully"]);
    } else {
        echo json_encode(["error" => "Error: " . $query . "<br>" . mysqli_error($conn)]);
    }
} else {
    echo json_encode(["error" => "Invalid request method"]);
}

mysqli_close($conn);
?>
