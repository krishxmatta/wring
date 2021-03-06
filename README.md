# wring
wring is a command line tool that leverages facial recognition to recognize who is present at a [Ring](https://ring.com/) video doorbell. It is designed to be self-hosted on a personal server.

## Installation
To install wring,
1. Clone the repository with `git clone https://github.com/krishxmatta/wring.git`
2. Enter the repository with `cd wring`
3. Install dependencies with `pip install -r requirements.txt`
4. Install wring with `python setup.py install`

## Usage
wring must first a config file saved as `~/.config/wring/config.yml` to be used. This config file must be structured as follows:

```
ring:
	email: <ring_email>
	password: <ring_password>
	verification_code: <ring_verification_code>
```

Ensure to fill in `ring/email` with your Ring account username, `ring/password` with your Ring account password, and `ring/verification_code` with your Ring verification code. This verification code can be generated by following [these instructions on the Ring site](https://support.ring.com/hc/en-us/articles/4401968771860-How-to-Generate-an-Alternate-Verification-Code-for-your-Ring-Account). Everytime a new verification code is generated, wring's config has to be properly updated.

People's faces can be entered into wring by simply creating the directory `~/.config/wring/img`. Within this `img` directory, make a directory for each person. This directory should have the name of the person. Then, within this directory, place a jpg file of the person's face; the image file name can be anything. For example, to enter John Doe's face into wring:

1. Ensure that the directory `~/.config/wring/img` exists
2. Make a new directory inside the `img` directory with John Doe's name: `mkdir ~/.config/wring/img/"John Doe"`
3. Place a jpg file of John Doe's face inside his directory: `mv john_doe.jpg ~/.config/wring/img/"John Doe"`

Once wring has been installed, a proper config file has been created, and faces are inputted into the program, wring can be invoked in the terminal with:

```
$ wring
```

This begins the wring client, which will run indefinitely and print any events that occur to any Ring doorbells associated with the device. If a doorbell is rang, then wring will analyze the camera video for people whose faces are inputted into the program. If a match is found, wring will print to the terminal that the found person is at the doorbell. If a match to a face is not found, but an unknown face is found, wring will print to the terminal that an unknown person is at your doorbell. An example log of wring is as follows:

```
$ wring
[2022-05-28 20:30:33.549335] Loading configuration...
[2022-05-28 20:30:33.551251] Loading faces...
[2022-05-28 20:30:45.640047] Connecting to Ring...
[2022-05-28 20:33:40.896460] Doorbell 'Front Door' has been rung
[2022-05-28 20:33:46.982956] Downloaded ring video for doorbell 'Front Door'
[2022-05-28 20:33:46.983092] Analyzing video for faces...
[2022-05-28 20:33:48.238693] Krish Matta is at Front Door!
```
