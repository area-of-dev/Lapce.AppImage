# Copyright 2022 Alex Woroschilow (alex.woroschilow@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
PWD:=$(shell pwd)

.PHONY: all

all: clean init
	mkdir --parents $(PWD)/build/Boilerplate.AppDir/lapce
	$(PWD)/bin/Apprepo.AppImage --destination=$(PWD)/build appdir boilerplate \
	    libreadline8

	wget https://github.com/lapce/lapce/releases/download/nightly/Lapce-linux.tar.gz  \
		--output-document=$(PWD)/build/build.tar.gz

	tar -xvf $(PWD)/build/build.tar.gz -C  \
		$(PWD)/build/

	cp --force $(PWD)/build/Lapce/*  $(PWD)/build/Boilerplate.AppDir/lapce
	chmod +x $(PWD)/build/Boilerplate.AppDir/lapce/lapce*

	echo ''                                                                >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                                                                >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'LD_LIBRARY_PATH=$${LD_LIBRARY_PATH}:$${APPDIR}/lapce'            >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'export LD_LIBRARY_PATH=$${LD_LIBRARY_PATH}'                      >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                                                                >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo ''                                                                >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo 'exec $${APPDIR}/lapce/lapce --wait "$${@}"'                      >> $(PWD)/build/Boilerplate.AppDir/AppRun


	chmod +x $(PWD)/build/Boilerplate.AppDir/AppRun
	rm --force $(PWD)/build/Boilerplate.AppDir/*.desktop || true

	cp --force $(PWD)/AppDir/*.desktop  $(PWD)/build/Boilerplate.AppDir/	
	cp --force $(PWD)/AppDir/*.png      $(PWD)/build/Boilerplate.AppDir/ || true
	cp --force $(PWD)/AppDir/*.svg      $(PWD)/build/Boilerplate.AppDir/ || true

	export ARCH=x86_64 && $(PWD)/bin/appimagetool.AppImage $(PWD)/build/Boilerplate.AppDir $(PWD)/Lapce.AppImage
	chmod +x $(PWD)/Lapce.AppImage

init:
	mkdir --parents $(PWD)/bin

	wget https://apprepo.de/appimage/download/apprepo \
		--output-document=$(PWD)/bin/Apprepo.AppImage
	chmod +x $(PWD)/bin/Apprepo.AppImage

	wget https://github.com/AppImage/AppImageKit/releases/download/13/appimagetool-x86_64.AppImage \
		--output-document=$(PWD)/bin/appimagetool.AppImage
	chmod +x $(PWD)/bin/appimagetool.AppImage

clean:
	rm -rf $(PWD)/*.AppImage
	rm -rf $(PWD)/bin/*
	rm -rf $(PWD)/build
