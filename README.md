# Overview
Using the [pigpio](http://abyz.me.uk/rpi/pigpio/) library, this repository will test the IR sensor & IR emitter of your MATRIX Creator by recording and playing back an IR signal you give it.

The example in this repository is taken from the [IR Record and Playback](http://abyz.me.uk/rpi/pigpio/examples.html#Python_irrp_py) pigpio example.

![](./demo.gif)

# Setup
This guide will be utilizing pins **13 & 16** of the Raspberry Pi. These pins are connected to the MATRIX Creator's **IR transmitter** & **IR receivers**, respectivly. For reference, below is an image of the Raspberry Pi GPIO connected to the MATRIX Creator.

![](https://matrix-io.github.io/matrix-documentation/matrix-creator/img/m-7.png)

## 1. Installing the MATRIX Dependencies
Keep in mind, that installing any of the [MATRIX Programming Environments](https://matrix-io.github.io/matrix-documentation/#programming-layers) will also include these MATRIX Dependencies.

Run the following commands in your Raspberry Pi's terminal to add the MATRIX repository & key and update your repository packages.
```bash
curl https://apt.matrix.one/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.matrix.one/raspbian $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/matrixlabs.list
```

Update your repositories and packages.
```bash
sudo apt-get update
sudo apt-get upgrade 
```

Install the MATRIX Creator init package.
```bash
sudo apt-get install matrixio-creator-init 
```

Reboot your Raspberry Pi.
```bash
sudo reboot
```

## 2. Installing pigpio
Once your Raspberry Pi has finished rebooting, go back into the terminal and run the following command to install pigpio.
```bash
sudo apt-get install pigpio
```

You will also need to install the python dependency with pip.
```bash
pip install pigpio
```

## 3. Downloading the IR Test
With all the required dependencies installed, you can now run the following commands to clone this repository in your Raspberry Pi.
```bash 
sudo apt-get install git
cd ~/
git clone https://github.com/matrix-io/matrix-creator-ir-test
cd matrix-creator-ir-test
```
## 4. Running the IR Test

When running this test you'll need to start the pigpio process.

**This must be done each time your Raspberry Pi boots.**
```bash
sudo pigpiod
```


Below are the test commands you can run.

- **Record**: This command allows you to specify the names of each IR signal you want to record. The command below will ask for 2 IR signals to signify the `channel_up & channel_down` and store them in a local file named `ir_codes.json`.
```bash
python ir_remote.py -r -g16 -f codes.json channel_up channel_down
```

- **Playback**: This command allows you to play any IR signal recorded with the previously mentioned command. The command below will play the IR signal that was stored as `channel_up` in `codes.json`
```bash
python ir_remote.py -p -g13 -f codes.json channel_up
```
