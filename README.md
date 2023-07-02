# instant_nerf
# 环境
- Windows: Visual Studio 2019 - Linux: GCC/G++ 7.5 or higher - CUDA v10.2 or higher - CMake v3.21 or higher. - (optional)OptiX 7.3 or higher - COLMAP

# 编译
打开develop command prompt for VS2019

`cd instant-ngp`

`cmake . -B build`

`cmake --build build --config RelWithDebInfo -j 16`

# 配置conda环境

`conda create -n ngp python=3.9`

`conda activate ngp`

`pip install -r requirements.txt`

`pip install OpenEXR-1.3.2-cp39-cp39-win_amd64.whl`


# 训练
#### step1: 视频解码与缩放
`python .\scripts\convert_video.py --input E:\NeRF\data\bottle\video.mp4  --output E:\NeRF\data\bottle\data\  --show_image 1 --scale 2`

#### step2：colmap重建，创建项目，选择图像路径以及数据库，
#### 分别进行特征提取/匹配/稀疏重建，导出稀疏模型文件
`colmap gui `

#### step3: 生成intant-ngp输入需要的transforms.json文件
`python scripts/colmap2nerf.py --aabb_scale 16 --images E:\NeRF\data\bottle\data --out E:\NeRF\data\bottle\transform.json`

# step4:  开始重建
`.\build\testbed.exe --scene E:\NeRF\real_data\data\tussock_tiny`


# 数据集路径
📂instant-ngp/ # this is root

├── 📂data/

│	├── 📂toy_truck/

│	│	├── 📜transforms.json # 这是要生成的文件

│	│	├── 📂data/

│	│	│	├── 📜image1.jpg

│	│	│	├── 📜image2.jpg


# 数据下载
链接：https://pan.baidu.com/s/1ht-RGNfDS-o7hj69LgUrFg 
提取码：gy36 
在目录nerf文件夹下有bottle数据

# 案例演示
链接：https://pan.baidu.com/s/1zfRJ9DO1NTdZeRnRAkxQrg 
提取码：tv5h 
在result_video目录下有两个三维重建时的视频。
