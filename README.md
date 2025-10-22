Absolutely ✅ — here’s a **clean, complete set of commands** and notes you can copy–paste for setting up Hyprland on **Ubuntu 25.10 (Questing Quokka)**, with correct cloning, configuration, installation, and remote reload instructions.

---

## 🧰 **Full Hyprland Setup for Ubuntu 25.10**

### 1️⃣ Clone the official 25.10 setup repo

```bash
cd ~
git clone -b 25.10 https://github.com/JaKooLit/Ubuntu-Hyprland.git ~/Ubuntu-Hyprland-25.10
cd ~/Ubuntu-Hyprland-25.10
```

*(This ensures you’re on the proper branch for Ubuntu 25.10 — newer Hyprland, correct scripts, and dependencies.)*

---

### 2️⃣ Install Hyprland and its dependencies

```bash
sudo add-apt-repository ppa:hyprland-dev/hyprland
sudo apt update
sudo apt install -y hyprland libhyprlang-dev libhyprutils-dev libhyprgraphics-dev
```

> 💡 This installs the latest stable **Hyprland 0.51+** and the required development libraries:
>
> * `libhyprlang` ≥ 0.6
> * `libhyprutils` ≥ 0.10
> * `libhyprgraphics` ≥ 0.2

---

### 3️⃣ Configure your monitors

Edit your Hyprland configuration file:

```bash
vi ~/.config/hypr/hyprland.conf
```

Add these lines (or update existing `monitor=` entries):

```bash
# Disable internal laptop screen
monitor=eDP-1,disable

# External monitor at 1440p ~60 Hz
monitor=HDMI-A-1,2560x1440@59.95,0x0,1
```

Save and exit (`:wq`).

---

### 4️⃣ Apply the new configuration locally

From within your graphical session:

```bash
hyprctl reload
```

✅ You’ll immediately see the laptop screen turn off and your external monitor activate at 2560×1440 @ 60 Hz.

---

### 5️⃣ (Optional) Apply configuration remotely via SSH

If you’re connected over SSH and want to reload Hyprland without being at the machine:

```bash
HYPRLAND_INSTANCE_SIGNATURE=$(ls /run/user/$(id -u)/hypr/ | head -n 1) hyprctl reload
```

💡 Tip: Add an alias for convenience:

```bash
echo "alias hyprreload='HYPRLAND_INSTANCE_SIGNATURE=\$(ls /run/user/\$(id -u)/hypr/ | head -n 1) hyprctl reload'" >> ~/.bashrc
source ~/.bashrc
```

Then just type:

```bash
hyprreload
```

---

### ✅ Quick Verification

* Check version:

  ```bash
  hyprland --version
  ```

  Should show something like:

  ```
  Hyprland 0.51.1
  hyprlang 0.6.3 | hyprutils 0.10.0 | hyprgraphics 0.2.0
  ```
* Confirm Wayland session:

  ```bash
  echo $XDG_SESSION_TYPE
  ```

  → `wayland`

---

### 🧠 TL;DR One-liner summary

```bash
cd ~ && git clone -b 25.10 https://github.com/JaKooLit/Ubuntu-Hyprland.git ~/Ubuntu-Hyprland-25.10
sudo add-apt-repository ppa:hyprland-dev/hyprland -y && sudo apt update
sudo apt install -y hyprland libhyprlang-dev libhyprutils-dev libhyprgraphics-dev
echo -e "\nmonitor=eDP-1,disable\nmonitor=HDMI-A-1,2560x1440@59.95,0x0,1" >> ~/.config/hypr/hyprland.conf
HYPRLAND_INSTANCE_SIGNATURE=$(ls /run/user/$(id -u)/hypr/ | head -n 1) hyprctl reload
```

---

Would you like me to extend this setup with a **floating window + deep shadow block** already included in `hyprland.conf`, so you can just paste it in one go?
