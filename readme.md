## Instal Vulkan SDK

### For linux
#### Ubuntu 20.04 (Focal Fossa)
```bash
wget -qO - http://packages.lunarg.com/lunarg-signing-key-pub.asc | sudo apt-key add -
sudo wget -qO /etc/apt/sources.list.d/lunarg-vulkan-focal.list http://packages.lunarg.com/vulkan/lunarg-vulkan-focal.list
sudo apt update
sudo apt install vulkan-sdk
```

### Create conanfile.txt
Added glfw lib