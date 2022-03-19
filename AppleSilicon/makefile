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

BUNDLE_LIBS := dylibbundler

# Directories
QUAKE_DIR  := ../Quake
LPROJ      := English.lproj
APP_EXE    := Quakespasm-SDL2-AppleSilicon.app
DISTRO_DIR := Quakespasm

APP_LIBS_DIR := $(APP_EXE)/Contents/libs

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

# Options
DEBUG := 0
AS_MK_OPTIONS := 

ifneq ($(DEBUG), 0)
	AS_MK_OPTIONS += DEBUG=1
endif

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
	$(BUNDLE_LIBS) -od -b -x ./$(APP_BINARY) -d ./$(APP_LIBS_DIR)/

compile:
	$(CD) $(QUAKE_DIR) && $(MAKE) -f $(APPLESILICON_MAKEFILE) $(AS_MK_OPTIONS)

distributable: app
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
	$(BREW) install pkg-config sdl2 opusfile mad mikmod vorbis-tools dylibbundler

clean_app: 
	-$(RM_DIR) $(APP_EXE)

clean: clean_app
	$(CD) $(QUAKE_DIR) && $(MAKE) -f $(APPLESILICON_MAKEFILE) clean
	-$(RM_DIR) $(DISTRO_DIR)
	-$(RM_DIR) libs
	-$(RM) $(DISTRO_ZIP)