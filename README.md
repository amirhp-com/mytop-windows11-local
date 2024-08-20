To use `mytop` on Windows 11, especially if you're working with Local by Flywheel (a local WordPress development environment), follow these steps:

### 1. **Install Windows Subsystem for Linux (WSL)**
WSL allows you to run a Linux distribution on Windows, which makes it easier to use Linux-based tools like `mytop`.

1. **Enable WSL:**
   Open PowerShell as Administrator and run:
   ```powershell
   wsl --install
   ```
   This command installs WSL and Ubuntu as the default Linux distribution. You can specify a different distribution if you prefer.

2. **Restart your computer** if prompted.

3. **Install Ubuntu**
   ```powershell
   wsl --install -d Ubuntu
   ```
4. **Open Ubuntu (or your chosen Linux distribution)**

### 2. **Install `mytop` in WSL**

Once your Linux distribution is set up:

1. **Update your package list**:
   ```bash
   sudo apt-get update
   // OR //
   sudo apt list --upgradable
   sudo apt upgrade
   ```

2. **Install `mytop`**:
   ```bash
   sudo apt-get install mytop
   // OR //
   sudo apt install mytop
   ```

### 3. **Connect to Local by Flywheel MySQL Database**

Local by Flywheel typically runs MySQL on a specific port on your localhost. You need to configure `mytop` to connect to this database.

1. **Find the MySQL credentials:**
   - Open Local by Flywheel.
   - Click on the site you're working on.
   - Go to the "Database" tab. You will find the credentials (username, password, host, port).

2. **Run `mytop` with the connection details**:
   ```bash
   mytop -u root -p -h 127.0.0.1 -P <port> -d <database_name>
   ```
   Replace `<port>` with the port number Local uses for MySQL, and `<database_name>` with the name of your database.

   For example, if the port is `3306` and the database name is `wordpress`:
   ```bash
   mytop -u root -p -h 127.0.0.1 -P 3306 -d wordpress
   ```

   After running the command, it will ask you for the MySQL root password (which you can find in Local's Database tab).

### 4. **Use `mytop`**

Once connected, `mytop` will display a real-time view of the queries running on your MySQL database. You can monitor slow queries, watch for locks, and get a sense of the overall activity.

### 5. **Optional: Create a Configuration File**

You can simplify the connection process by creating a `.mytop` configuration file in your home directory:

```bash
nano ~/.mytop
```

Add the following content (adjust with your credentials):
```plaintext
user=root
pass=<your_password>
host=127.0.0.1
db=<database_name>
port=<port>
delay=5
```

Now, you can simply run `mytop` without additional parameters.

---

By following these steps, you should be able to monitor live MySQL queries on your local environment using `mytop` in a WSL environment on Windows 11.
