
# 🚀 Chat Application Using IPC and Signals

Welcome to the **Chat Application** repository! This project demonstrates a simple chat application implemented in C using Inter-Process Communication (IPC) mechanisms like shared memory and signals.

## 📋 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Analysis](#analysis)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## 📖 About the Project

This application facilitates real-time communication between two users, demonstrating the use of shared memory and signals for IPC. The project consists of two main components:

- **User 1 (Client-Side)**
- **User 2 (Server-Side)**

## ✨ Features

- Real-time messaging between two processes
- Efficient use of shared memory for message storage
- Signal handling for notification of new messages and chat termination
- Proper resource management and cleanup

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed on your system:

- GCC compiler (for compiling C programs)
- Linux-based OS (recommended for IPC features)

### Installation

1. **Clone the Repository**
   \`\`\`sh
   git clone https://github.com/your-username/chat-application-ipc-signals.git
   \`\`\`
2. **Navigate to the Project Directory**
   \`\`\`sh
   cd chat-application-ipc-signals
   \`\`\`
3. **Compile the Code**
   \`\`\`sh
   gcc -o user1 user1.c -lrt
   gcc -o user2 user2.c -lrt
   \`\`\`

## 🎮 Usage

1. **Run User 1 (Client-Side)**
   \`\`\`sh
   ./user1
   \`\`\`

2. **Run User 2 (Server-Side)**
   \`\`\`sh
   ./user2
   \`\`\`

3. **Messaging**
   - User 1 and User 2 can send and receive messages in real-time.
   - Type "Q\n" to end the chat session.

## 🗂 Project Structure

\`\`\`
├── user1.c      # Client-side source code
├── user2.c      # Server-side source code
├── README.md    # Project documentation
└── LICENSE      # License file
\`\`\`

## 🔍 Analysis of IPC-based Chat Application

### **Overview**

This chat application, implemented in C, enables real-time communication between two users using Inter-Process Communication (IPC) through shared memory and signals.

### **🔄 Shared Memory**

- **Definition & Purpose**: Shared memory acts as a common area for message exchange between processes.
- **Setup**: It is initialized using a unique key (`12345`) and organized using a `struct memory` that includes a message buffer, a status flag, and process IDs.

### **🚦 Status Flags**

- **FILLED (0)**: Indicates the buffer has a new message ready for reading.
- **Ready (1)**: Indicates the buffer is available for writing a new message.
- **NotReady (-1)**: Indicates the buffer is not ready for communication.

### **🔔 Signal Handling**

- **Mechanism**: Uses signals (`SIGUSR1` and `SIGUSR2`) to notify processes of new messages or chat termination.
- **Handlers**:
  - User 1 listens for `SIGUSR1`.
  - User 2 listens for `SIGUSR2`.

### **🔄 Program Flow**

#### **👤 User 1 (Client-Side)**

1. **Initialization**: Sets up shared memory, assigns `pid1`, and sets the status to `NotReady`. Installs a signal handler for `SIGUSR1`.
2. **Message Loop**:
   - Waits for `Ready` status.
   - Accepts user input, sets status to `FILLED`, and notifies User 2.
   - Ends chat on "Q\n" input, detaches, and removes shared memory.

#### **👥 User 2 (Server-Side)**

1. **Initialization**: Similar to User 1, sets up shared memory, assigns `pid2`, and status to `NotReady`. Installs a signal handler for `SIGUSR2`.
2. **Message Loop**:
   - Awaits user input when status is not `Ready`.
   - Sets status to `Ready` and notifies User 1.
   - Awaits status change, indicating User 1's response.

### **💡 Conclusion**

The application efficiently utilizes shared memory and signals to enable synchronized message exchange between two processes, ensuring smooth communication. The code demonstrates resource management best practices, including proper memory detachment and cleanup.

### **🔧 Potential Enhancements**

- **Security**: Implement authentication to secure shared memory access.
- **Scalability**: Extend the architecture to support multiple users or chat rooms.
- **User Interface**: Develop a graphical interface for better user experience.

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request for any improvements or features.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/feature-name`)
3. Commit your Changes (`git commit -m 'Add some feature'`)
4. Push to the Branch (`git push origin feature/feature-name`)
5. Open a Pull Request

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

Your Name - [your-email@example.com](mailto:your-email@example.com)

Project Link: [https://github.com/your-username/chat-application-ipc-signals](https://github.com/your-username/chat-application-ipc-signals)
