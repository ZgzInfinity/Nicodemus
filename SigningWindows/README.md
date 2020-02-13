<p align="center">
    <img src="https://ibb.co/tKmKv8L" alt="Logo" width=100height=100>
  </a>

  <h3 align="center">Linux</h3>

  <p align="center">
    <b>Signing commits in Windows</b> <br>
  </p>
</p>

In order to sign our commits in Windows you must proceed as follows:

* First of all, we need to install a Git client such as **GitHub Desktop** on our Windows operating system. This tool can be easily downloaded from the following websites, respectively.
	* https://desktop.github.com/
 
It doesn't have to be the previous ones, you can choose the  one you like best.

* After this step, you'll proceed to downloading for the Git Bash  tool, which can be found at the following link:

	* https://gitforwindows.org/

		This software provides to the user the following features:

		* **Git BASH:** Git for Windows provides a BASH emulation used to run Git from the command line. *NIX users should feel right at home, as the BASH emulation behaves just like the "git" command in LINUX and UNIX environments.

		* **Git GUI**: As Windows users commonly expect graphical user interfaces, Git for Windows also provides the Git GUI, a powerful alternative to Git BASH, offering a graphical version of just about every Git command line function, as well as comprehensive visual diff tools.

		* **Shell Integration**: Simply right-click on a folder in Windows Explorer to access the BASH or GUI.

* Once the tool is installed you will proceed to run it and you should see a window like the one below with your own user name: 

<p align="center">
    <img src="https://i.ibb.co/L5w9z9v/bash.png">
</p>

* This command GitHub supports several GPG key algorithms. If you try to add a key generated with an unsupported algorithm, you may encounter an error.

	-   RSA
	-   ElGamal
	-   DSA
	-   ECDH
	-   ECDSA
	-   EdDSA

-   Now, you must generate a GPG key pair. To do that, you must be aware about that:
    
    -   If you are on version 2.1.17 or greater, paste the text below to generate a GPG key pair.
        
        ``
        $ gpg --full-generate-key
     ``

    -   If you are not on version 2.1.17 or greater, the `gpg --full-generate-key` command doesn't work. Paste the text below and skip to step 6.
        
		 ``
     $ gpg --default-new-key-algo rsa4096 --gen-key
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
   <img src="https://i.ibb.co/L1gv9bq/clave-ejemplo.png">
</p>
	
* Exexute this command substituting in the GPG key ID what key you would like to use. In this example they key is  `3B3AF4BD7A3BEBDB`.
    ```
    $ gpg --armor --export 3B3AF4BD7A3BEBDB
    ```
 This command prints the GPG key ID, in ASCII armor format.

* Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----.
* The next step is to add your new GPG key to your github account. In order to get this, you must must follow these steps:
	* Open your github account and go to the option **settings** in your profile.

		<p align="center">
	    <img src="https://i.ibb.co/TcgnrWW/settings.png">
	</p>

	*	Go to the SSH and GPG keys option.
			
		<p align="center">
	    <img src="https://i.ibb.co/FJfDCP2/options.png">
	</p>

	*	Select the button **New GPG key** and introduced what you selected before in the box. Finally, press **Add GPG key** button. You should see in your screen something like this:
	
		<p align="center">
	    <img src="https://i.ibb.co/4R841P7/clave.png">
	</p>

* The next step is configure Gitby editing the `.gitconfig` file. In order to do that you can execute this command: 
 `git config --global --edit` in a terminal, then replace 
    
	* **github_email:** the email address used to login on Github
	* **signing_key:** the GPG key  used to sign commits.
	* **gpg_binary_path:** the GPG binary file path, depending on your Git install and your operating system:
    `C:\\Program Files\\Git\\usr\\bin\\gpg.exe` is the path in Windows by default, but if you are not sure you can check it with the command `where gpg`.

	In my case the file would be like this:

	<p align="center">
	    <img src="https://i.ibb.co/93NYBjm/clave.png">
	</p>

3.  Enjoy **signed commits** with your favorite code editor.

Be careful. This only makes possible commit with sign verification if the passphrase is introduced. If you want to avoid this you must introduced the following command:

`git config --global commit.gpgsign true`