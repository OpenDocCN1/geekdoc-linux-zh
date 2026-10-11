```

		header("Location: " . $config_basedir);
		break;
	}
	else {
		require("header.php");
		echo "This account is not verified yet. You were emailed a link to verify the account. Please click on the link in the email to continue.";
	}
	echo "This account is not verified yet. You were emailed a link to verify the account. Please click on the link in the email to continue.";
	}
	else {
		header("Location: " . $config_basedir . "/login.php?error=1");
	}
}

```

If a login error occurs, the page is redirected, and error=1 is added as a GET variable. This can be used to add an error message:

```

	else {
		header("Location: " . $config_basedir . "/login.php?error=1");
	}
} else {
	require("header.php");

	if($_GET['error']) {
		echo "Incorrect login, please try again!";
	}
?>
<form action="<?php echo pf_script_with_get($SCRIPT_NAME); ?>" method="post">

```

Finally, add the footer:

Don't have an account? Go and <a href="register.php">Register</a>!

```

<?php
}
require("footer.php");
?>

```