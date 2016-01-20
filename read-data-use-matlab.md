install matlab-lmdb api from github
-----------
* use git to clone the [codes](https://github.com/kyamagu/matlab-lmdb) and build on matlab

  ```shell
  git clone https://github.com/kyamagu/matlab-lmdb.git
  ```
* build and test

  ```shell
  matlab
  ```
  ```matlab
  addpath /home/chenweilun/Downloads/matlab-lmdb; %this should be the directory where you store codes.
  lmdb.make();
  lmdb.make('test')
  ```
  now you have successfully installed matlab api for lmdb.

read features in lmdb database
-----------
