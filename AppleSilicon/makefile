# Commands
MAKE   := make
BREW   := brew
CD     := cd
CP     := cp
CP_DIR := cp -r
RM	   := rm
RM_DIR := rm -r
MKDIR  := mkdir -p
TOUCH  := touch
ECHO   := echo
ZIP    := zip -r -X
INT    := install_name_tool

# Directories
QUAKE_DIR  := ../Quake
LPROJ      := English.lproj
APP_EXE    := Quakespasm-SDL2-AppleSilicon.app
DISTRO_DIR := Quakespasm

BREW_PREFIX := $(shell brew --prefix)

# Files
APPLESILICON_MAKEFILE := Makefile.applesilicon
ID1_NOTIF_FILE := put_id1_here!!!.txt

EXE        := quakespasm
APP_BINARY := $(APP_EXE)/Contents/MacOS/Quakespasm
PLIST      := Info.plist
PKGINFO    := PkgInfo
ICON       := QuakeSpasm.icns
DISTRO_ZIP := Quakespasm.zip
QS_MUSIC   := ../Quakespasm-Music.txt
QS_TXT     := ../Quakespasm.txt
QS_HTML    := ../Quakespasm.html
QS_LICENSE := ../LICENSE.txt
QS_PAK     := $(QUAKE_DIR)/quakespasm.pak

# Other
ID1_NOTIF := "Copy your id1 folder from your Steam/CD install of Quake into this folder, and make sure id1/pak0.pak and id1/pak1.pak are lower case!"

# Targets
all: app
	
app: compile
	$(MKDIR) $(APP_EXE)
	$(MKDIR) $(APP_EXE)/Contents
	$(MKDIR) $(APP_EXE)/Contents/MacOS
	$(MKDIR) $(APP_EXE)/Contents/Resources
	$(CP) $(PLIST) $(APP_EXE)/Contents
	$(CP) $(PKGINFO) $(APP_EXE)/Contents
	$(CP) $(ICON) $(APP_EXE)/Contents/Resources
	$(CP) $(QUAKE_DIR)/$(EXE) $(APP_BINARY)
	$(CP_DIR) $(LPROJ) $(APP_EXE)/Contents/Resources
	# TODO: Don't hard code these paths. Build libs for macOS 11.0 and add binaries to project
	$(CP_DIR) $(BREW_PREFIX)/opt/flac/lib/libFLAC*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/flac/lib/libFLAC.8.dylib @executable_path/libFLAC.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/opus/lib/libopus*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/opus/lib/libopus.0.dylib @executable_path/libopus.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/opusfile/lib/libopusfile*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/opusfile/lib/libopusfile.0.dylib @executable_path/libopusfile.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/libogg/lib/libogg*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/libogg/lib/libogg.0.dylib @executable_path/libogg.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/libvorbis/lib/libvorbisfile*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/libvorbis/lib/libvorbisfile.3.dylib @executable_path/libvorbisfile.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/libvorbis/lib/libvorbis*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/libvorbis/lib/libvorbis.0.dylib @executable_path/libvorbis.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/mad/lib/libmad*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/mad/lib/libmad.0.dylib @executable_path/libmad.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/libmikmod/lib/libmikmod*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/libmikmod/lib/libmikmod.3.dylib @executable_path/libmikmod.dylib $(APP_BINARY)
	$(CP_DIR) $(BREW_PREFIX)/opt/sdl2/lib/libSDL2*.dylib $(APP_EXE)/Contents/MacOS
	$(INT) -change /opt/homebrew/opt/sdl2/lib/libSDL2-2.0.0.dylib @executable_path/libSDL2.dylib $(APP_BINARY)
	$(INT) -change /opt/homebrew/opt/libvorbis/lib/libvorbisfile.3.dylib @executable_path/libvorbisfile.dylib $(APP_EXE)/Contents/MacOS/libvorbisfile.dylib
	$(INT) -change /opt/homebrew/Cellar/libvorbis/1.3.7/lib/libvorbis.0.dylib @executable_path/libvorbis.dylib $(APP_EXE)/Contents/MacOS/libvorbisfile.dylib
	$(INT) -change /opt/homebrew/opt/libogg/lib/libogg.0.dylib @executable_path/libogg.dylib $(APP_EXE)/Contents/MacOS/libvorbisfile.dylib

signed_app: app
	sudo codesign -s - -f $(APP_EXE)/Contents/MacOS/libvorbisfile.dylib
	sudo codesign -s - -f $(APP_BINARY)

compile:
	$(CD) $(QUAKE_DIR) && $(MAKE) -f $(APPLESILICON_MAKEFILE)

distributable: signed_app
	$(MKDIR) $(DISTRO_DIR)
	$(CP_DIR) $(APP_EXE) $(DISTRO_DIR)
	$(TOUCH) $(DISTRO_DIR)/$(ID1_NOTIF_FILE)
	@$(ECHO) $(ID1_NOTIF) > $(DISTRO_DIR)/$(ID1_NOTIF_FILE)
	$(CP) $(QS_MUSIC) $(DISTRO_DIR)
	$(CP) $(QS_TXT) $(DISTRO_DIR)
	$(CP) $(QS_HTML) $(DISTRO_DIR)
	$(CP) $(QS_PAK) $(DISTRO_DIR)
	$(CP) $(QS_LICENSE) $(DISTRO_DIR)

zip: distributable
	$(ZIP) $(DISTRO_ZIP) $(DISTRO_DIR)

install_libs:
	$(BREW) install sdl2 opusfile mad mikmod vorbis-tools

clean:
	$(CD) $(QUAKE_DIR) && $(MAKE) -f $(APPLESILICON_MAKEFILE) clean
	-$(RM_DIR) $(APP_EXE)
	-$(RM_DIR) $(DISTRO_DIR)
	-$(RM) $(DISTRO_ZIP)