# This were the steps followed to build the rpm
1. Clone this repo
```
git clone git@github.com:egarbi/perl-Net-Amazon-S3-rpm.git
```
2. Download and Extract the content of the old package 
```
cd perl-Net-Amazon-S3-rpm
rpm2cpio.pl /some/path/perl-Net-Amazon-S3-0.80-1.of.el7.noarch.rpm | cpio -idmv
```
3. Check for pre/post building scripts
```bash
rpm -qp --scripts perl-Net-Amazon-S3-0.80-1.of.el7.noarch.rpm
```
4. Clone (or fetch) the latest version from mantainer
```
git clone https://github.com/rustyconover/net-amazon-s3.git
```
5. Sync the proper files
```
rsync -az net-amazon-s3/lib/Net/Amazon/* usr/share/perl5/vendor_perl/Net/Amazon/
rsync -az ~/net-amazon-s3/bin/s3cl usr/bin/s3cl
cp ~/net-amazon-s3/CHANGES README.md usr/share/doc/perl-Net-Amazon-S3-0.81/
```
6. Build the new rpm, the file can be find on builds/ dir
```
fpm --verbose \
  -s dir \
  -t rpm \
  -p builds/ \
  -n perl-Net-Amazon-S3 -v 0.84 \
  -m quique@enriquegarbi.com.ar \
  --url 'https://github.com/egarbi/perl-Net-Amazon-S3-rpm' \
  -a noarch \
  --description 'Simple Storage Service from Perl' \
  usr/=/usr/
```
