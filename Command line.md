# 1. VẬN HÀNH OPENSTACK
1. Hiển thị thông tin các image

`openstack image list`

2. Tạo volume boot

`openstack volume create --bootable --image image_id--description vm_name--size size_in_GB--type volume_type_name vm_name`

3. Tạo volume

`openstack volume create --description volume_name --size size_in_GB --type volume_type_namevolume_name`

4. Hiển thị thông tin các volume

`openstack volume list`

5. Hiển thị thông tin các flavor

`openstack flavor list`

6. Hiển thị thông tin các network

`openstack network list`

7. Hiển thị thông tin các zone

`openstack availability zone list`

8. Hiển thị thông tin các host

`openstack host list`

9. Hiển thị thông tin các hypervisor

`openstack hypervisor list`

10. Tạo VM

`openstack server create --flavor flavor_id--availability-zone zone_name:host_name--volume volume_id--nic net-id=network_id--user-data path_cloudinit_filevm_name`

11. ADD volume vào VM

`openstack server add volume vm_id volume_id`

12. Hiển thị thông tin các VM 

`openstack server list`

13. Migrate VM giữa các host khác đời cpu

`openstack server migrate --os-compute-api-version 2.56 --host host_name vm_id`

# 2. Tao Project, User, thêm User vào Project, cập nhập Quota cho Project
1. Khởi tạo project

- B1: Tạo project với quyền admin

  `admin-openrc`
  `openstack project create --description new --domain default --enable CNTT1`

  với các thông tin sau:

  - Description: Trung tâm CNTT
  - Domain: default
  - Trạng thái: enable 
  - Tên project: CNTT1
- B2: Xóa project

`openstack project delete <project_id>`

- B3: Kiểm tra project đã tạo

`openstack project list`

2. Khởi tạo người dùng

- B1: Kiểm tra danh sách user

`openstack user list`

- B2: Tạo user

  `openstack user create --domain default --project CNTT1 --password 123123Aa --description new --enable newuser`

  Thông tin người dùng:
  - Domain: default
  - Project: chọn project chính quản lý user đã tạo(ở đây là CNTT1)
  - Password: Nhập password
  - Description: mô tả user
  - Enable: cho phép user hoạt động
  - User name: tên user
  - Email: mail người dùng 

- B3: Xóa user

`openstack user delete <user-name-or-id>`

- B4: Kiểm tra các role hiện có

`openstack role list`

- B5: Kiểm tra user hiện có 

`openstack user list`

- B6: Gán role cho member hiện có vào project

`openstack role add --user newuser --project newproject member`

- B7: Xóa role khỏi user

`openstack role remove --user newuser --project newproject user`

3. Cập nhập quota trên project
- B1: xem quota hiện tại trên project

`openstack quota show`

- B2: Cập nhập quota cho project

`openstack quota set<resoure><project_id>`

# 3 Tạo, xem  và xóa flavor 

- B1: Xem danh sách flavor

`openstack flavor list`

- B2: Tạo flavor

`openstack flavor create <name> --id <id> --vcpu <vcpus> --ram <size-mb> --disk <size-gb> --ephemeral <size-gb> --swap <size-mb>`

  Ví dụ: 

  `openstack flavor create newflavor --id auto --vcpu 4 --ram 4096  --disk 0 --ephemeral 0 --swap 0`

  *Lưu ý: Đối với các máy bảo boot từ volume(SAN Storage), cần taoh flavor với Root Disk và Ephemeral Disk(GB) là 0* 

- B3: Xóa Flavor

`optenstack flavor delete<flavor_id>`

# 4 Tạo image
- B1: Tạo image

  `openstack image create --disk-format qcom2 --min-disk 0 --min-ram 0 --file /root/cirros-0.3.4-x84_64-disk.img --unprotected --public Cirros-4`
 
  - --disk-format: chọn định dạng cho image (ở đây đang là qcow2)
  - --min-disk: chọn minimum disk (ở đây đang là 0)
  - --min-ram: chọn minimum ram (ở đây đang là 0)
  - --file: chọn đường dẫn đến image muốn boot hệ điều hành
  - --unprotected: chọn chế độ không "protected" image (ta có thể chỉnh thành tùy chọn protected bằng "--protected")
  - --public: chọn chia sẻ image cho các project hoặc user khác
  - Cirros-4: đây là tên image

- B2: Xem danh sách image đã tạo

`optenstack image list`

- B3: Xóa image 

`openstack image delete <image id>`
