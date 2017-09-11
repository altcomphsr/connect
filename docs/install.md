# Installation

Wir stellen für diverse Distributionen vorgefertigte Pakete zur Verfügung.
Du solltest wann immer möglich diese Pakete verwenden, denn damit bekommst du auch bequem Updates. Eine manuelle Installation bedeutet auch manuelle Updates.

Solltest du ein exotisches Betriebssystem verwenden oder einfach aus Spass den open\HSR-connect von Hand installieren, dann kannst du wie folgt vorgenen.

Führe folgende Befehle als root aus!

## Für Linux-Distributionen:

###Sync
1. Install dependencies

    ```
    $ sudo apt-get install git python3-setuptools gcc python3-dev libffi-dev libssl-dev python3-pip -y
    ```

2. Clone repo

    ```
    $ git clone https://github.com/openhsr/connect.git
    $ cd connect
    ```
	
3. Build & install

    ```
    $ sudo  python3 ./setup.py install
    ```
	
4. Set up sync settings

    ```
    $ openhsr-connect edit
    ```
	
    Enter HSR information, modify config file for your classes ([See example configuration](https://github.com/openhsr/connect/blob/master/docs/config.example.yaml))

5. Profit!

    ```
    $ openhsr-connect sync
    ```
	
    Sync the specified directories with the script server.

	
### Drucker
Damit CUPS das E-Mail-Backend nutzen kann muss dieses verlinkt werden.

```bash
ln -s $INSTALLATIONSPFAD/openhsr_connect/resources/openhsr-connect /usr/lib/cups/backend/openhsr-connect
```

Zudem müssen die Berechtigungen angepasst werdenn:

```bash
chmod 700 /usr/lib/cups/backend/openhsr-connect
chown root:root /usr/lib/cups/backend/openhsr-connect
```

Nun muss auch ein Drucker eingerichtet werden.
```bash
# Add the printer if not yet installed
lpstat -a openhsr-connect 2&> /dev/null
if [ $? -ne 0 ]; then
    echo "Adding printer openhsr-connect"
    lpadmin -p openhsr-connect -E -v openhsr-connect:/tmp -P $INSTALLATIONSPFAD/openhsr_connect/resources/Generic-PostScript_Printer-Postscript.ppd
fi
```


Dieser kann bei einer deinstallation wie folgt entfernt werden:
```bash
lpstat -a openhsr-connect 2&> /dev/null
if [ $? -eq 0 ]; then
    echo "Removing printer openhsr-connect"
    lpadmin -x openhsr-connect
fi
```
## Für macOS:

### Sync

1. Install [Homebrew](http://brew.sh/)

    ```
    $/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```
	

2. Install Python 3

    ```
    $ brew install python3
    ```

3. Clone repo

    ```
    $ git clone https://github.com/openhsr/connect.git
    $ cd connect
    ```

	
4. Build & install

    ```
    $ python3 ./setup.py install
    ```

	
5. Set up sync settings

    ```
    $ openhsr-connect edit
    ```
	
    Enter HSR information, modify config file for your classes ([See example configuration](https://github.com/openhsr/connect/blob/master/docs/config.example.yaml))
    If you get a decoding error and the application crashes after entering your email address, make sure you have your encoding set to 'Western (ISO Latin 1)' and not UTF-8. You can change this setting under Terminal->Preferences->Profiles->Advanced->Text encoding.

6. Profit!

    ```
    $ openhsr-connect sync
    ```
	
    Sync the specified directories with the script server.

### Drucker
Damit CUPS das E-Mail-Backend nutzen kann muss dieses verlinkt werden.
```bash
ln -s $INSTALLATIONSPFAD/openhsr_connect/resources/openhsr-connect /usr/libexec/cups/backend/openhsr-connect
```

Zudem müssen die Berechtigungen angepasst werdenn:

```bash
chmod 700 /usr/libexec/cups/backend/openhsr-connect
chown root:wheel /usr/libexec/cups/backend/openhsr-connect
```

Nun muss auch ein Drucker eingerichtet werden.
```bash
# Add the printer if not yet installed
lpstat -a openhsr-connect 2&> /dev/null
if [ $? -ne 0 ]; then
    echo "Adding printer openhsr-connect"
    lpadmin -p openhsr-connect -E -v openhsr-connect:/tmp -P $INSTALLATIONSPFAD/openhsr_connect/resources/Generic-PostScript_Printer-Postscript.ppd
fi
```


Dieser kann bei einer deinstallation wie folgt entfernt werden:
```bash
lpstat -a openhsr-connect 2&> /dev/null
if [ $? -eq 0 ]; then
    echo "Removing printer openhsr-connect"
    lpadmin -x openhsr-connect
fi
```

##Für Windows (Not officially supported)

### Sync
1. Download Python 3.x

    Latest is 3.5.2 as of creation of this guide. [Download website](https://www.python.org/downloads/release/python-352/), [Installer](https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe))
    Install and make sure to install the py launcher as well (this setting should automatically be set in the advanced installation options).

2. Install git

    [Download link](https://git-scm.com/download/win)

3. Clone repo

    Open admin command prompt

    ```
    $ git clone https://github.com/openhsr/connect.git
    $ cd connect
    ```
	

4. Build & install

    ```
    $ py -3 setup.py install
    ```
	

5. Add Python Scripts folder to $PATH

    For x64 Python this path is ```C:\Program Files\Python35\Scripts``` by default. If you're not sure how to add this to Path, check [this link](http://www.computerhope.com/issues/ch000549.htm)

6. Set up sync settings

    ```
    $ openhsr-connect edit
    ```
	
    Enter HSR information, modify config file for your classes (See example [here](https://github.com/openhsr/connect/blob/master/docs/config.example.yaml))

7. Profit!

    ```
    $ openhsr-connect sync
    ```
	
    Sync the specified directories with the script server.

##Bash on Ubuntu on Windows (Not officially supported)
### Sync
It's probably easier to just use it in Windows if you're on Windows but here's how you'd get it to work on BoUoW:

Follow steps 1-3 from the Ubuntu/Debian section, then:

Download & install keyrings.alt

```
$ cd
$ curl https://pypi.python.org/packages/27/d0/9207bf58de11735fe2239deaecb9eae1084e2887077a700ac8aa27bd8159/keyrings.alt-1.1.1.tar.gz | tar xz
$ cd keyrings.alt-1.1.1
$ sudo python3 ./setup.py install
```

Continue with step 4 from the Linux-Distributionen section.

