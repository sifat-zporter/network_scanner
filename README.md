# network_scanner

Scan configured local IP ranges and identify devices on the network. The scanner uses nmap results plus optional MAC address mappings to attach friendly names and manufacturer details.

## Features

- Scan a user-defined IP range in CIDR or range notation.
- Check multiple IP ranges from different subnets.
- Map MAC addresses to custom device names and manufacturers.
- Update device information on a scheduled basis when used by an integrating application.
- Report the devices found during a scan.

## Installation

Clone the project and install it in a virtual environment:

```bash
git clone https://github.com/your-org/network_scanner.git
cd network_scanner
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e .
```

Install the nmap executable separately. On Debian or Ubuntu:

```bash
sudo apt-get update
sudo apt-get install nmap
```

On macOS with Homebrew:

```bash
brew install nmap
```

**The Python package and the nmap executable are separate requirements.** Confirm that nmap is available before running a scan:

```bash
nmap --version
```

## Usage

Run a scan against one CIDR range and provide a MAC address mapping:

```bash
python -m network_scanner \
  --ip-range "192.168.1.0/24" \
  --mapping "bc:14:14:f1:81:1b;Brother Printer;Cloud Network Technology Singapore Pte. Ltd."
```

A mapping uses this format:

```text
MAC address;friendly name;manufacturer
```

For multiple ranges, pass the ranges separated by spaces:

```bash
python -m network_scanner \
  --ip-range "10.100.1.0/24 10.1.1.0/24" \
  --mapping "bc:14:14:f1:81:1b;Brother Printer;Cloud Network Technology Singapore Pte. Ltd." \
  --mapping "b1:81:11:31:a1:b1;My iPhone;Apple Inc."
```

The scanner needs network access to the selected ranges. Depending on the scan options and host operating system, nmap may also require elevated permissions.

## License

This project is licensed under the MIT License.

`network_scanner` is based on [parvez/network_scanner](https://github.com/parvez/network_scanner), an MIT-licensed Home Assistant network scanner integration. See the original project for attribution and license details.

