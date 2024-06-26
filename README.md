Password Checks in PHP
======================

1\. Password Length Check
-------------------------

PHP Code:

    <?php
    if (strlen($password) < 8) {
        $message = "Password is too short (8 characters minimum)";
        return false;
    }
    ?>
    

This code checks if the password is at least 8 characters long.

Example:

*   Password: **Pass1!** (Length: 6) - This will fail with the message "Password is too short (8 characters minimum)".
*   Password: **SecurePassword1!** (Length: 16) - This will pass the length check.

2\. Password Complexity Check
-----------------------------

PHP Code:

    <?php
    $complexity = 0;
    if (preg_match("/([a-z]+)/", $password)) $complexity++;
    if (preg_match("/([A-Z]+)/", $password)) $complexity++;
    if (preg_match("/([0-9]+)/", $password)) $complexity++;
    if (preg_match("/([^a-zA-Z0-9]+)/", $password)) $complexity++;
    if ($complexity < 3) {
        $message = "Password is not complex enough (use uppercase, lowercase and numbers)";
        return false;
    }
    ?>
    

This code ensures the password contains at least three different types of characters: lowercase letters, uppercase letters, numbers, and special characters.

Example:

*   Password: **password** - Contains only lowercase letters (Complexity: 1) - This will fail with the message "Password is not complex enough (use uppercase, lowercase and numbers)".
*   Password: **Password1** - Contains lowercase letters, uppercase letters, and numbers (Complexity: 3) - This will pass the complexity check.

3\. Username Check
------------------

PHP Code:

    <?php
    if (stripos($password, $username) !== false) {
        $message = "Password should not contain the username";
        return false;
    }
    ?>
    

This code checks if the password contains the username.

Example:

*   Username: **johndoe**
*   Password: **JohnDoe2023!** - This will fail with the message "Password should not contain the username".
*   Password: **Secure2023!** - This will pass the username check.

4\. Full Name Parts Check
-------------------------

PHP Code:

    <?php
    $nameParts = explode(' ', $fullName);
    foreach ($nameParts as $part) {
        if (strlen($part) > 2 && stripos($password, $part) !== false) {
            $message = "Password should not contain parts of the full name";
            return false;
        }
    }
    ?>
    

This code checks if the password contains any parts of the user's full name that are longer than two characters.

Example:

*   Full Name: **Jane Smith**
*   Password: **Smith2023!** - This will fail with the message "Password should not contain parts of the full name".
*   Password: **Secure2023!** - This will pass the full name parts check.