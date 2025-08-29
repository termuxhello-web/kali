#!/data/data/com.termux/files/usr/bin/bash

echo "[*] Cập nhật Termux & cài proot-distro..."
pkg update -y && pkg install -y proot-distro git wget curl termux-api pulseaudio tigervnc

termux-wake-lock
settings put global stay_on_while_plugged_in 3

echo "[*] Cài Kali Linux..."
proot-distro install kali

echo "[*] Đổi tên Kali -> nethunter-x"
proot-distro rename kali nethunter-x

echo "[*] Tải script cài tool..."
wget -O /data/data/com.termux/files/home/.nethunter-post.sh https://raw.githubusercontent.com/ten-ban/nethunter-x/main/config/postinstall.sh
chmod +x ~/.nethunter-post.sh

echo "[*] Chạy postinstall trong Kali..."
proot-distro login nethunter-x -- bash /root/.nethunter-post.sh

echo "[*] Tạo lệnh chạy GUI..."
cat > ~/start-nethunter-gui.sh <<EOF
#!/data/data/com.termux/files/usr/bin/bash
export PULSE_SERVER=127.0.0.1
pulseaudio --start --exit-idle-time=-1
proot-distro login nethunter-x --start-command "vncserver :1 -geometry 1280x720 -depth 24"
EOF

chmod +x ~/start-nethunter-gui.sh
echo "[+] Hoàn tất! Chạy ./start-nethunter-gui.sh để vào Kali GUI."
