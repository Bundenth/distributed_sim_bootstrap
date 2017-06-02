# Bootstrap Distributed Simulator singularity image
# OS: Ubuntu 1
# Packages: 
#  - OpenMPI 2.0.1 DONE
#  - GCC 4.9. DONE
#  - METIS DONE
#  - Scalasca NOT DONE

BootStrap: debootstrap
OSVersion: trusty
MirrorURL: http://us.archive.ubuntu.com/ubuntu/

%post
	echo "** Installing requested packages...."
	apt-get -y install software-properties-common #python-software-properties
	add-apt-repository ppa:ubuntu-toolchain-r/test
	apt-get update
	apt-get -y install wget gcc-4.9 g++-4.9 make cmake nano
	update-alternatives --remove-all gcc 
	update-alternatives --remove-all g++
	update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 20
	update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 20
	update-alternatives --config gcc
	update-alternatives --config g++
	#echo "** Install OFED libraries for HPC"
        #apt-get -y install --reinstall language-pack-en
	#locale-gen en_US.UTF-8
	#wget http://www.openfabrics.org/downloads/OFED/ofed-3.5-2/OFED-3.5-2.tgz
        #tar xvf OFED-3.5-2.tgz
        #cd OFED-3.5-2
        #./install.pl
	#cd ..
	#rm OFED-3.5-2.tgz
	echo "** Install OpenMPI"
	wget https://www.open-mpi.org/software/ompi/v2.0/downloads/openmpi-2.0.1.tar.gz
	tar xvf openmpi-2.0.1.tar.gz
	cd openmpi-2.0.1
	mkdir build
	cd build
	../configure --prefix=/usr/local
	make all install
	cd ..
	cd ..
	rm openmpi-2.0.1.tar.gz
	echo "** Install METIS"
	wget http://glaros.dtc.umn.edu/gkhome/fetch/sw/metis/metis-5.1.0.tar.gz
	tar xvf metis-5.1.0.tar.gz
	cd metis-5.1.0
	cd include
	sed -i 's/IDXTYPEWIDTH 32/IDXTYPEWIDTH 64/g' metis.h
	cd ..
	make config # installs it in /usr/local
	make
	make install
	cd ..
	rm metis-5.1.0.tar.gz
	ldconfig	
