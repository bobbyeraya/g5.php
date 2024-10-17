g5.php
<?php
session_start(); // Start the session

// Initialize visit count for the session
if (!isset($_SESSION['visit_count'])) {
    $_SESSION['visit_count'] = 0;
}
$_SESSION['visit_count']++;

// Initialize total visit count
if (isset($_COOKIE['total_visits'])) {
    $total_visits = $_COOKIE['total_visits'] + 1; // Increment total visits
} else {
    $total_visits = 1; // First visit
}
setcookie('total_visits', $total_visits, time() + (86400 * 30), "/"); // Cookie expires in 30 days

// Check if a team member has been viewed and store it in the session
if (isset($_GET['member'])) {
    $_SESSION['last_viewed_member'] = htmlspecialchars($_GET['member']);
}

// Team members array
$team_members = [
    [
        'name' => 'John Carlo Conte',
        'position' => 'Leader',
        'bio' => 'Visionary design leader with a track record of inspiring teams, driving innovation, and delivering impactful solutions that elevate brand identity and user experience.',
        'img' => 'pics/p1.jpg.jpg',
        'facebook' => 'https://www.facebook.com/profile.php?id=100090557971785&mibextid=ZbWKwL',
        'instagram' => 'https://www.instagram.com/jay_zieee?igsh=MTZiaTJwanlweGNoOQ=='
    ],
    [
        'name' => 'Hansel Dela Paz - Sauler',
        'position' => 'Developer',
        'bio' => 'An invaluable asset for developers provides clear requirements, timely feedback, and essential resources, facilitating efficient problem-solving and project success.',
        'img' => 'pics/h2.jpg',
        'facebook' => 'https://www.facebook.com/hansel.dlpz',
        'instagram' => 'https://www.instagram.com/heeyhans?igsh=d3FmYzV0bjEwa2Rq&utm_source=d3FmYzV0bjEwa2Rq'
    ],  
    [
        'name' => 'Bobby Eraya',
        'position' => 'Support',
        'bio' => 'Experienced design support professional offering expertise in project management, feedback integration, and technical assistance to enhance design workflows and outcomes.',
        'img' => 'pics/n1.jpg',
        'facebook' => 'https://www.facebook.com/profile.php?id=100012508365639',
        'instagram' => 'https://www.instagram.com/erayabobby?igsh=dzV1d2Z5eXpicm9o'
    ],  
    [
        'name' => 'Jahafar C. Albain',
        'position' => 'Designer',
        'bio' => 'Creative designer specializing in engaging visuals and strategic branding, committed to transforming ideas into compelling, user-centered designs.',
        'img' => 'pics/jaff.jpg',
        'facebook' => 'https://www.facebook.com/Hittimaru',
        'instagram' => 'https://www.instagram.com/ndntfd_jxff/'
    ],  
    [
        'name' => 'Mikaela Staples',
        'position' => 'Designer',
        'bio' => 'Accessible mentor, offering constructive feedback, clear guidance, and valuable resources to empower designers and enhance their skills.',
        'img' => 'pics/wewe.jpg',
        'facebook' => 'https://www.facebook.com/profile.php?id=100009431208267&mibextid=LQQJ4d',
        'instagram' => 'https://www.instagram.com/itssssmikayyy?igsh=MWJqeGw4ajNwaWxmZA%3D%3D&utm_source=qr'
    ],  
];
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TEAM PROFILE G5</title>
    <link rel="stylesheet" type="text/css" href="g5.css">
</head>
<body>

    <header>
        <h1>Meet Our Team</h1>
        <p>This website has been visited <?php echo isset($_COOKIE['total_visits']) ? $_COOKIE['total_visits'] : 1; ?> times.</p>
    </header>
    <main>
        <?php foreach ($team_members as $member): ?>
            <section class="team-member" onclick="openModal(
                '<?php echo $member['name']; ?>', 
                '<?php echo $member['position']; ?>', 
                '<?php echo $member['bio']; ?>', 
                '<?php echo $member['img']; ?>',
                '<?php echo $member['facebook']; ?>',
                '<?php echo $member['instagram']; ?>'
            )">
                <img src="<?php echo $member['img']; ?>" alt="<?php echo $member['name']; ?>">
                <h2><?php echo $member['name']; ?></h2>
                <p><?php echo $member['position']; ?></p>
            </section>
        <?php endforeach; ?>
    </main>
    <footer>
        <p>&copy; 2024 Our Company. All rights reserved.</p>
        <p>Created this for Groupings</p>
    </footer>
    <div id="teamModal" class="modal">
        <div class="modal-content">
            <button class="close-btn" onclick="closeModal()">&times;</button>
            <img id="modalImg" src="" alt="Team Member">
            <h2 id="modalName"></h2>
            <p id="modalPosition"></p>
            <p id="modalBio"></p>
            <div class="social-buttons">
                <a id="modalFacebook" href="" target="_blank" class="social-button">Facebook</a>
                <a id="modalInstagram" href="" target="_blank" class="social-button">Instagram</a>
            </div>
        </div>
    </div>

    <script type="text/javascript">
        function openModal(name, position, bio, imgSrc, facebook, instagram) {
            document.getElementById('modalName').textContent = name;
            document.getElementById('modalPosition').textContent = 'Position: ' + position;
            document.getElementById('modalBio').textContent = bio;
            document.getElementById('modalImg').src = imgSrc;
            document.getElementById('modalFacebook').href = facebook;
            document.getElementById('modalInstagram').href = instagram;

            // Pass the team member name as a query parameter for the session
            window.history.pushState({}, '', '?member=' + encodeURIComponent(name));

            document.getElementById('teamModal').style.display = 'flex';
        }

        function closeModal() {
            document.getElementById('teamModal').style.display = 'none';
        }
    </script>
</body>
</html>
