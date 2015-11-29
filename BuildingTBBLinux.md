Building Threading Building Blocks from source is easy:
  1. Download the source from the 'Download' section of [the TBB website](http://threadingbuildingblocks.org/) (I chose the latest Commercial Aligned Release, which was 3.0 update 5).
  1. Un-tar the archive.
  1. Build it with your favorite compiler. If you omit the `compiler=icc` parameter to `make` the system's default compiler is used.

```
cd
wget http://threadingbuildingblocks.org/uploads/78/165/3.0%20Update%205/tbb30_131oss_src.tgz
tar -zxvf tbb30_131oss_src.tgz
mv tbb30_131oss ~/src/

cd ~/src/tbb30_131oss/
make compiler=icc
```