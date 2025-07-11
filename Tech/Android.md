
## Introduction to Android
- Android is an open-source mobile operating system developed by Google.
- It is built on the Linux kernel and designed for touchscreen devices (smartphones, tablets, etc.).
- Supports millions of apps through the Google Play Store.
- Written primarily in Java and Kotlin.

---

## Key Features:
- Open-source and customizable
- Wide device compatibility
- Rich APIs for UI, camera, GPS, sensors, etc.
- Backed by Google with regular updates

---
## Linux OS vs Android OS 

1. **Linux OS** is a general-purpose operating system used in desktops, servers, and embedded systems.  
   **Android OS** is a mobile operating system built on top of the Linux kernel, mainly for smartphones and tablets.

2. **Linux** uses desktop environments like **GNOME** or **KDE**, while **Android** has its own **touch-based user interface**.

3. **Linux applications** are usually written in **C/C++** and run natively,  
   whereas **Android apps** are written in **Java/Kotlin** and run using the **Android Runtime (ART)**.

4. **Linux OS** provides **full system access** to users and developers,  
   while **Android OS** uses **sandboxing** to isolate each app for better security.

5. **Linux** uses traditional package formats like `.deb` or `.rpm`,  
   while **Android** uses `.apk` files to install apps.

6. **Linux** accesses hardware **directly** via device drivers,  
   whereas **Android** uses a **Hardware Abstraction Layer (HAL)** between the system and hardware.

7. **Linux** boot process typically starts with **BIOS/UEFI → Bootloader → Kernel → Init**,  
   while **Android** starts with **Bootloader → Kernel → Zygote → System Server → Apps**.

8. In Linux we have **IPC** mechanisms to communicate between two processes,
   In android we have **Binder IPC** to communicate between two processes.

---

## Android Architecture:

![Android](https://github.com/user-attachments/assets/08e8b711-0bd3-4a01-bee1-11178397e4bf)

## Android Applications:
- This is the layer where all the apps run.
- It includes:
  - **Pre-installed apps** like Phone, Camera, Contacts, and Gallery.
  - **Downloaded apps** from the Play Store like WhatsApp, Instagram, and games.
- These apps run inside the **Android Runtime**.
- They use the **Application Framework** below them to access features like camera, storage, and internet.
![image](https://github.com/user-attachments/assets/c5d355b4-8a81-482c-a5a1-7f374922c1b9)

## Android API

- **API** stands for **Application Programming Interface**.
- The Android API is a set of tools and commands that developers use to build apps.
- It provides **ready-made functions** to interact with device features like:
  - Camera
  - Bluetooth
  - Location (GPS)
  - Wi-Fi
  - Sensors
- Instead of writing low-level code, developers just **call these APIs** to get things done quickly and efficiently.
- This makes app development **easier, faster, and more reliable**.

## Privileged Apps

- These are **special system apps** that have more access than regular apps.
- They are usually **pre-installed** by the device manufacturer or Android itself.
- They can perform **sensitive tasks** that normal apps can't do, like:
  - Managing phone calls
  - Accessing system settings
  - Controlling device security
- Privileged apps are **trusted by the system** and often stored in a secure part of the device.
- Example apps: **Phone app, Settings app, System UI**

## Device Manufacturer Apps

- These apps are created by the **device manufacturer** (e.g., Samsung, Xiaomi, OnePlus).
- They come **pre-installed** on the phone and are tailored to that device's hardware and features.
- Examples:
  - Samsung Notes
  - MI Camera App
  - OnePlus File Manager
- They often have access to **extra system features** and use special APIs.
- These apps help manufacturers offer a **customized experience** on their devices.


## System Services

- These are **background services** that help Android run smoothly.
- They provide **core functions** needed by both the system and apps.
- Apps and other system parts use these services to get work done.
- Examples of system services include:
  - **Activity Manager** – manages app activities and lifecycles.
  - **Power Manager** – controls battery and power usage.
  - **Package Manager** – handles app installation and updates.
  - **Window Manager** – manages the display and app windows.
- These services make sure that everything on your Android device works **efficiently and reliably**.

  ## Application Framework

- The Application Framework gives **tools and services** to app developers.
- It helps developers **build apps easily** without writing everything from scratch.
- It allows apps to use device features like:
  - Camera
  - Screen display
  - Storage
  - Location
- It includes important parts like **Activity Manager**, **Notification Manager**, and more, which help apps work properly.

## Android Runtime (ART)

- The Android Runtime is a **core part of the Android system** that helps apps run.
- It includes:
  - **Core libraries** that provide features used in Java and Kotlin.
  - A virtual machine (like Dalvik or ART) to run app code.
- It works like the **Java Virtual Machine (JVM)** but is specially designed for Android.
- It allows Android to run **multiple apps smoothly and efficiently**.
- It uses the **Linux Kernel** for tasks like memory management and multitasking.
- Because of this, developers can build apps using **Java or Kotlin** programming languages.

![image](https://github.com/user-attachments/assets/5fe8ee2a-69cc-4b65-a661-00be62b91ef5)


**Zygote**

- **Zygote** is a special process in Android that helps apps start faster.
- When the device boots, Zygote is launched and loads all common libraries and resources into memory.
- When a new app is opened, it **forks (copies) from Zygote**, which saves time and memory.
- This makes app launching **quick and efficient**.

**Core Libraries (in Android Runtime)**

- Core Libraries are a set of **essential pre-built packages** used to build Android apps.
- They provide support for the **Java/Kotlin programming languages** and Android system features.

**Core Libraries Include:**

- **Java core packages**:
  - `java.lang` – basic classes like `String`, `Object`
  - `java.util` – collections, date/time, utilities
  - `java.io` – file and input/output operations

- **Android-specific packages**:
  - `android.app` – components like `Activity`, `Service`
  - `android.content` – for `Intent`, `BroadcastReceiver`, etc.
  - `android.view` and `android.widget` – for UI elements (buttons, layouts, etc.)

**Why They Are Important:**

- Help developers write apps in **Java or Kotlin** without needing to build everything from scratch.
- Enable access to core Android features like UI, storage, communication, and system services.

## Hardware Abstraction Layer (HAL)

- HAL stands for **Hardware Abstraction Layer**.
- It acts as a **bridge between the Android system and device hardware**.
- HAL lets Android talk to hardware components like:
  - Camera
  - GPS
  - Bluetooth
  - Wi-Fi
  - Sensors
- Instead of writing code for each hardware device, HAL provides a **standard way** to access them.
- Every hardware feature has its own **HAL module** (e.g., camera HAL, audio HAL).

## Native Daemons and Libraries

**Native Daemons**
- These are **background system programs** written in **C/C++**.
- They perform **low-level tasks** and run independently.
- Common functions:
  - Managing **Wi-Fi and Bluetooth**
  - Handling **media playback**
  - Supporting **file system** operations
- They work closely with the **Linux Kernel** and **HAL** to support hardware features.

**Native Libraries**
- Native Libraries are **pre-built C/C++ libraries** used by the Android system and apps.
- They provide **core functionalities** like:
  - `libc` – Standard C library
  - `OpenGL` – Graphics rendering
  - `libmedia` – Audio/video support
  - `SQLite` – Lightweight database
- These libraries help Android apps and services run **faster and more efficiently**.
![image](https://github.com/user-attachments/assets/9ba017b9-22a2-4b3f-a1c6-ef385e7b0c38)

**Platform Libraries**

- **Platform Libraries** are the core libraries provided by the Android system.
- They include both:
  - **Native libraries** (written in C/C++)
  - **Managed libraries** (written in Java/Kotlin)
- These libraries help apps and system components access essential Android features like UI, networking, storage, graphics, and more.

## Linux Kernel

- The **Linux Kernel** is the **core (heart)** of the Android operating system.
- It acts as a **bridge between the hardware** and the rest of the Android software.
- It manages important system tasks like:
  - **Memory** – how much space apps can use
  - **Power** – battery usage and power control
  - **Processes** – running and switching between apps
  - **Drivers** – like camera, display, audio, Bluetooth, etc.

**Key Features of the Linux Kernel:**

- **Security** – Keeps apps and the system protected from each other.
- **Memory Management** – Efficiently handles memory use by apps.
- **Process Management** – Allocates resources to apps and manages them.
- **Network Stack** – Manages all internet and data communication.
- **Driver Model** – Lets Android work with different hardware using built-in drivers.

![image](https://github.com/user-attachments/assets/7ae9c6d0-6378-47fa-885f-8d54ff519a36)

---
## Difference Between Linux and Android Architecture

| Feature                  | Linux Architecture                                      | Android Architecture                                             |
|--------------------------|---------------------------------------------------------|------------------------------------------------------------------|
| **Main Purpose**         | General-purpose OS (desktop/server)                    | Designed for **mobile/embedded devices**                         |
| **User Interface**       | GUI (GNOME/KDE) or Command Line                         | Android-specific UI (Activities, Views)                          |
| **Applications**         | Linux native apps                                       | APK apps built with Android SDK                                 |
| **System Libraries**     | GNU/Linux libraries                                     | Java core libraries + native C/C++ libraries                     |
| **Runtime**              | No specific runtime                                     | Android Runtime (ART) and Dalvik (older)                         |
| **Hardware Access**      | Direct via drivers/modules                              | Through **HAL (Hardware Abstraction Layer)**                     |
| **Package Format**       | `.deb`, `.rpm`                                          | `.apk`                                                           |          |
| **Boot Process**         | BIOS → Bootloader → Kernel → Init                       | Bootloader → Kernel → **Zygote** → System Server → App           |


---

## What is Booting?
Booting is the process of starting or restarting the system by loading the operating system into memory.

---
## Types of Boot
**Hard Boot**
- It is also called as cold boot.
- Booting a system from a powered off state.
- Happens when the device is turned on.
- **Example:** Turning on your PC using the power button.

---
**Soft Boot**
- It is also called as warm boot.
- Restarting the system without turning off the power.
- Triggered by OS restart, reset button, or a software command.
- **Example:** Clicking Restart in Windows.

---
**Dual Boot**
- Booting into more than one OS (user selects one during startup).
- Example: Windows + Linux on one machine.

---
**Fast Boot**
- Fast Boot is a feature that reduces boot time by skipping certain hardware checks and initializations during startup.
- Skips some initial checks (like POST) to speed up the booting process.

---
**Secure Boot**
- Secure Boot is a security feature that prevents unauthorized or malicious code from running during the boot process.
- A UEFI feature that ensures only trusted software is loaded during boot.

---

## Android Boot Process (When You Power On)

- **Bootloader:** Initializes hardware and loads the kernel.  
- **Linux Kernel:** Starts managing CPU, memory, drivers.  
- **Init:** Android’s init process starts system services (like Wi-Fi, Bluetooth).  
- **Zygote:** A special process that loads common app code (Java libraries) and starts apps quickly by forking.  
- **System Server:** Starts Android’s core services (WindowManager, PackageManager, etc.).  
- **Home/Launcher App:** The main screen you see (with icons and widgets) starts.  

---
## Difference betwwen Linux boot and Android boot

| Feature                  | Linux Boot Process                                    | Android Boot Process                                     |
|--------------------------|--------------------------------------------------------|-----------------------------------------------------------|
| **Target Devices**       | Desktops, Servers, Embedded Systems                    | Smartphones, Tablets, Smart Devices                       |
| **Operating System Type**| General-purpose OS                                     | Mobile OS based on Linux kernel                           |
| **Bootloader**           | GRUB, LILO, U-Boot                                     | Android Bootloader with Fastboot support                  |
| **Kernel**               | Standard Linux kernel                                  | Modified Linux kernel with mobile-specific changes        |
| **Init System**          | `systemd`, `SysVinit`, `Upstart`                       | Android `init` with `.rc` configuration scripts           |
| **Root Filesystem**      | Uses `/`, `/etc`, `/home` (ext4, xfs, etc.)            | Uses `/system`, `/vendor`, `/data` (ext4, YAFFS2, F2FS)   |
| **Boot Image Format**    | Separate `vmlinuz` (kernel) and `initrd`               | Single `boot.img` (kernel + ramdisk + DTB)                |
| **Startup Services**     | Daemons like `sshd`, `cron`, `networkd`                | `system_server`, `Zygote`, Android Framework services     |
| **Java Runtime**         | Optional (only when installed)                         | Core component (Zygote spawns ART/Dalvik runtime)         |
| **App Launch Mechanism** | Standard process execution                             | Apps launched by forking Zygote process                   |
| **Recovery Mode**        | Not standard; may require custom setup                 | Dedicated Recovery Partition                              |
| **Fastboot Mode**        | Not typical                                             | Standard bootloader mode for flashing and debugging       |
| **Secure Boot**          | UEFI Secure Boot (optional, PC-specific)               | Verified Boot (dm-verity, AVB enforced on most devices)   |
| **Update Mechanism**     | Package managers (`apt`, `yum`) or scripts             | OTA updates, often with A/B partitioning scheme           |
| **Filesystem Structure** | Conventional Linux hierarchy                           | Partition-based (boot, system, vendor, recovery, etc.)    |
| **Target Users**         | Developers, Sysadmins, General Users                   | End Users, App Developers, OEMs                           |

---
## Interview Questions
- what is Android?
- Difference between Linux os and Android os.
- Explain about Android Architecture.
- Explain about Android booting Process.

---

## Downloading and Building Source code
- repo init manifest.xml
- repo sync
- cd apps/LINUX/android
- source build/envsetup.sh
- lunch devicename-variantname
   **ex:** lunch tinker-user
- make
## Build variants
- **userdebug:** Engineering build W/O root(possible to root) and it is used for testing and debugging.
- **user:** production build W/O root(different kernel config).
- **eng:** Engineering build W/root.
   
    

    
