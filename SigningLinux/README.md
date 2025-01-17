<p align="center">
    <img src="https://i.ibb.co/0rCwRBp/gnulinux.jpg" alt="Logo" width=100height=100>
  </a>

  <h3 align="center">Linux</h3>

  <p align="center">
    <b>Signing commits in Linux</b> <br>
  </p>
</p>

&nbsp;


This technique is very similar to the last one. Nevertheless, we dont have any tool to create the GPG keys like in Windows due to we can use directly the terminal. If you want to sign your commits with your Linux distribution you must follow the next steps:

* First of all, you have to open a terminal a generate a pair of GPG keys with the following command:

``
	gpg --full-generate-key
``

After entering the command, you will be asked to validate the followings parameters:

* The kind of key you want to generate, among the previous ones. In this case I used RSA which is the default option. 
	* The size of the key. In my case I selected 4096 bits.
	*  Time period in which the key is valid. In my case is the option 0 (forever).
	* Finally, it requests confirmation of the above steps. So you must introduce y if you agree or n if you disagree.

	Subsequently, you must introduce the following information in order to construct a user ID to identify your key. 

	*	**Real Name**: In my case I used ZgzInfinity.
	*	**Email Addres**: You must use the email that is configured to link your commits.
	*	**An optional comment**: you can enter whatever you want.
	* Finally, you must confirm all the steps.

	Then, you must introduce a **passphrase** to protect your new key and confirm it.

	Use the `gpg --list-secret-keys --keyid-format LONG` command to list GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.
You should show in your terminal something like this:

	<p align="center">
	    <img src="https://i.ibb.co/7CwvMm0/fff.png">
	</p>

* Exexute this command substituting in the GPG key ID what key you would like to use. In this example they key is  `580C3E61CC32CA3E`.
    ```
    $ gpg --armor --export 580C3E61CC32CA3E
    ```
	 This command prints the GPG key ID, in ASCII armor format.

* Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----.
* The next step is to add your new GPG key to your github account. In order to get this, you must must follow these steps:
	* Open your github account and go to the option **settings** in your profile.

		<p align="center">
	    <img src="https://i.ibb.co/TcgnrWW/settings.png">
	</p>

	* Go to the SSH and GPG keys option.
			
		<p align="center">
	    <img src="https://i.ibb.co/FJfDCP2/options.png">
	</p>

	* Select the button **New GPG key** and introduced what you selected before in the box. Finally, press **Add GPG key** button. You should see in your screen something like this:
	
		<p align="center">
	    <img src="https://i.ibb.co/2dc9FZM/temas.png">
	</p>

* The next step is configure Gitby editing the `.gitconfig` file. In order to do that you can execute this command: 
 `git config --global --edit` in a terminal, then replace 
    
	* **github_email:** the email address used to login on Github
	* **signing_key:** the GPG key  used to sign commits.
	* **gpg_binary_path:** the GPG binary file path, depending on your Git install and your operating system:
    `/usr/bin/gpg` is the path in Windows by default, but if you are not sure you can check it with the command `whereis gpg`.

	In my case the file would be like this:

	<p align="center">
	    <img src="https://i.ibb.co/r48m8WJ/configuration.png">
	</p>

3.  Enjoy **signed commits** with your favorite code editor.

Be careful. This only makes possible a signed commit if the passphrase is introduced. In order to auto-sign all commits globaly introduce this command:

`git config --global commit.gpgsign true`