# Peter Moss Acute Myeloid & Lymphoblastic Leukemia AI Research Project
## OneAPI Acute Lymphoblastic Leukemia Classifier
### OneAPI OpenVINO Raspberry Pi 4 Acute Lymphoblastic Leukemia Classifier

![OneAPI OpenVINO Raspberry Pi 4 Acute Lymphoblastic Leukemia Classifier](../../Media/Images/Peter-Moss-Acute-Myeloid-Lymphoblastic-Leukemia-Research-Project.png)

&nbsp;

# Table Of Contents

- [Installation](#installation)
	- [Prerequisites](#prerequisites)
      - [HIAS Server](#hias-server)
      - [OneAPI Acute Lymphoblastic Leukemia Classifier CNN](#oneapi-acute-lymphoblastic-leukemia-classifier-cnn)
      - [Intermediate Representation](#intermediate-representation)
      - [Raspberry Pi Buster](#raspberry-pi-buster)
    - [Intel® Distribution of OpenVINO™ Toolkit](#intel-distribution-of-openvino-toolkit)
      - [Intel® Movidius™ Neural Compute Stick 2](#intel-movidius-neural-compute-stick-2)
	- [HIAS iotJumpWay](#clone-the-repository)
	- [Clone The Repository](#clone-the-repository)
	- [Setup File](#setup-file)
	- [Continue](#continue)
- [Contributing](#contributing)
  - [Contributors](#contributors)
- [Versioning](#versioning)
- [License](#license)
- [Bugs/Issues](#bugs-issues)

# Installation
This guide will take you through installing the requirements for the OneAPI Acute Lymphoblastic Leukemia Classifier.

## Prerequisites
Before you can install this project, there are some prerequisites.

### HIAS Server
For this project you will need a functioning [HIAS Server](https://github.com/LeukemiaAiResearch/HIAS). To install the HIAS Server, follow the [HIAS Server Installation Guide](https://github.com/LeukemiaAiResearch/HIAS/blob/master/Documentation/Installation/Installation.md)

### OneAPI Acute Lymphoblastic Leukemia Classifier CNN
For this project you will use the model created in the [CNN](../../CNN "CNN") project. If you would like to train your own model you can follow the CNN guide, or you can use the pre-trained model and weights provided in the [Model](../Model "Model") directory.

### Intermediate Representation
If you are training the model yourself, you need to convert your model to an Intermediate Representation so that it can be used with OpenVINO and the Neural Compute Stick 2.

To do this, once you have finished the OneAPI Acute Lymphoblastic Leukemia Classifier CNN tutorial, use the following commands, replacing **PathToProject** with the path to the CNN project:

```
 cd C:\Program Files (x86)\IntelSWTools\openvino\bin\
  setupvars.bat
  cd C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\model_optimizer
 python3 mo_tf.py --input_model PathToProject\Model\Freezing\frozen.pb --input_shape [1,100,100,3] --output_dir PathToProject\Model\IR --reverse_input_channels --generate_deprecated_IR_V7
```
The Intermediate Representation for your model will now be accessible in the [CNN project IR directory](../../CNN/Model/IR), you need to copy these files to your Raspberry Pi in the same location in the RPI4 Model directory.

### Raspberry Pi Buster
For this Project, the operating system choice is [Raspberry Pi Buster](https://www.raspberrypi.org/downloads/raspberry-pi-os/ "Raspberry Pi Buster"), previously known as Raspian.

## Intel® Distribution of OpenVINO™ Toolkit
To install Intel® Distribution of OpenVINO™ Toolkit for Raspberry Pi, navigate to the home directory on your Raspberry Pi and use the following commands:

```
  wget https://download.01.org/opencv/2020/openvinotoolkit/2020.4/l_openvino_toolkit_runtime_raspbian_p_2020.4.287.tgz
  sudo mkdir -p /opt/intel/openvino
  sudo tar -xf  l_openvino_toolkit_runtime_raspbian_p_2020.4.287.tgz  --strip 1 -C /opt/intel/openvino
  sudo apt install cmake
  source /opt/intel/openvino/bin/setupvars.sh
  echo "source /opt/intel/openvino/bin/setupvars.sh" >> ~/.bashrc
```

### Intel® Movidius™ Neural Compute Stick 2
Now we will set up ready for Neural Compute Stick 2.
```
  sudo usermod -a -G users "$(whoami)"
```
Now close your existing terminal and open a new open. Once in your new terminal use the following commands:
```
  sh /opt/intel/openvino/install_dependencies/install_NCS_udev_rules.sh
```

## HIAS iotJumpWay
![HIAS iotJumpWay](../Media/Images/iotJumpWay-Device-Create.png)

You will need a HIAS iotJumpWay device to run this application. Log in to your HIAS Server UI and navigate to **IoT->Devices** and click on the **+** button to create a new device.

Fill in the details and once you click **Create** you will be provided with the credentials for your iotJumpWay device. Make sure you save the Blockchain password as you will not be able to recover or change them in the future, the other credenitials you will be able to retrieve through the device page and/or reset them.

Open the configuration file [config.json](../Model/config.json) and fill in your HIAS iotJumpWay and HIAS iotJumpWay device details.

```
  "iotJumpWay": {
      "host": "",
      "port": 8883,
      "ip": "localhost",
      "ipinfo": "",
      "lid": 0,
      "zid": 0,
      "did": 0,
      "dn": "",
      "un": "",
      "pw": ""
  }
```

## Clone the repository
Clone the [OneAPI Acute Lymphoblastic Leukemia Classifier](https://github.com/AMLResearchProject/oneAPI-ALL-Classifier " OneAPI Acute Lymphoblastic Leukemia Classifier") repository from the [Peter Moss Acute Myeloid & Lymphoblastic Leukemia AI Research Project](https://github.com/AMLResearchProject "Peter Moss Acute Myeloid & Lymphoblastic Leukemia AI Research Project") Github Organization.

To clone the repository and install the OneAPI Acute Lymphoblastic Leukemia Classifier Classifier, make sure you have Git installed. Now navigate to the a directory on your device using commandline, and then use the following command.

```
 git clone https://github.com/AMLResearchProject/oneAPI-ALL-Classifier.git
```

Once you have used the command above you will see a directory called **oneAPI-ALL-Classifier** in your home directory.

```
 ls
```

Using the ls command in your home directory should show you the following.

```
 oneAPI-ALL-Classifier
```

Navigate to **oneAPI-ALL-Classifier/RPI4** directory, this is your project root directory for this tutorial.

### Developer Forks

Developers from the Github community that would like to contribute to the development of this project should first create a fork, and clone that repository. For detailed information please view the [CONTRIBUTING](../../CONTRIBUTING.md "CONTRIBUTING") guide. You should pull the latest code from the development branch.

```
 git clone -b "0.5.0" https://github.com/AMLResearchProject/oneAPI-ALL-Classifier.git
```

The **-b "0.5.0"** parameter ensures you get the code from the latest master branch. Before using the below command please check our latest master branch in the button at the top of the project README.

## Setup File

All other requirements are included in **Setup.sh**. You can run this file on machine by navigating to the **RPI4** directory in terminal and using the commands below:

```
 sed -i 's/\r//' Setup.sh
 sh Setup.sh
```

# Continue
Now you can continue with the [OneAPI OpenVINO Raspberry Pi 4 Acute Lymphoblastic Leukemia Classifier tutorial](../README.md#getting-started)

&nbsp;

# Contributing

The Peter Moss Acute Myeloid & Lymphoblastic Leukemia AI Research project encourages and youlcomes code contributions, bug fixes and enhancements from the Github.

Please read the [CONTRIBUTING](../../CONTRIBUTING.md "CONTRIBUTING") document for a full guide to forking our repositories and submitting your pull requests. You will also find information about our code of conduct on this page.

## Contributors

- [Adam Milton-Barker](https://www.leukemiaresearchassociation.ai/team/adam-milton-barker "Adam Milton-Barker") - [Asociacion De Investigacion En Inteligencia Artificial Para La Leucemia Peter Moss](https://www.leukemiaresearchassociation.ai "Asociacion De Investigacion En Inteligencia Artificial Para La Leucemia Peter Moss") President/Lead Developer, Sabadell, Spain

&nbsp;

# Versioning

You use SemVer for versioning. For the versions available, see [Releases](../../releases "Releases").

&nbsp;

# License

This project is licensed under the **MIT License** - see the [LICENSE](../../LICENSE.md "LICENSE") file for details.

&nbsp;

# Bugs/Issues

You use the [repo issues](../../issues "repo issues") to track bugs and general requests related to using this project. See [CONTRIBUTING](../../CONTRIBUTING.md "CONTRIBUTING") for more info on how to submit bugs, feature requests and proposals.