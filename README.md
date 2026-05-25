# Distributed File Conversion Service

## Short Description
This project is a distributed file conversion system built with Python sockets and TLS.
A client uploads a file to a central server, the server assigns the job to an available worker, and the converted file is sent back to the client.

The current implementation supports JPG to PNG image conversion and CSV to JSON conversion.

## Features
- Distributed architecture with separate client, server, and worker processes.
- Secure communication using TLS/SSL sockets.
- Job scheduling on the server side.
- Worker pool management to handle available and busy workers.
- File upload and download between client, server, and worker.
- Supported conversions:
  - `.jpg` to `.png`
  - `.csv` to `.json`

## Tech Stack
- Python 3
- `socket` module for network communication
- `threading` for concurrent handling of clients and jobs
- `ssl` for encrypted communication
- `Pillow` for image conversion
- `csv` and `json` for CSV to JSON conversion

## Installation and Setup
1. Clone the repository and open the `Distributed-File-Conversion-Service` folder.
2. Create a Python virtual environment if you want to keep dependencies isolated.
3. Install the required package:

	```bash
	pip install Pillow
	```

4. Generate or place a TLS certificate and private key for the server.
	The server expects `cert.pem` and `key.pem` inside the `server` folder.
5. Update the host configuration if needed:
	- `client/config.py` should point to the server IP or `localhost`.
	- `worker/config.py` should point to the same server address.

## Usage
Run the application in three parts:

1. Start the server:

	```bash
	cd server
	python server.py
	```

2. Start one or more workers in separate terminals:

	```bash
	cd worker
	python worker.py
	```

3. Start the client and provide the path of the file to convert:

	```bash
	cd client
	python client.py
	```

After the client connects, enter the file path when prompted. The server queues the request, assigns it to an available worker, and returns the converted file to the client.

## Project Structure
```text
Distributed-File-Conversion-Service/
├── client/
│   ├── client.py
│   ├── config.py
│   └── file_transfer.py
├── server/
│   ├── client_handler.py
│   ├── config.py
│   ├── file_transfer.py
│   ├── scheduler.py
│   ├── server.py
│   └── worker_manager.py
├── worker/
│   ├── config.py
│   ├── converter.py
│   ├── file_transfer.py
│   └── worker.py
├── LICENSE
└── README.md
```

## Future Improvements
- Add support for more file formats such as PDF, DOCX, and TXT
- Store uploaded and converted files in dedicated folders instead of the project root
- Provide a web-based or GUI client for a simpler user experience
- Handle edge cases where the server or a worker fails during file transfer or conversion


