PKG_NAME = Radarr
PKG_VERS = 3.0.0.4204
PKG_EXT = tar.gz
PKG_DIST_NAME = v$(PKG_VERS).$(PKG_EXT)
PKG_DIST_FILE = $(PKG_NAME)-$(PKG_VERS).$(PKG_EXT)
PKG_DIST_SITE = https://github.com/Radarr/Radarr/archive
PKG_DIR = $(PKG_NAME)-$(PKG_VERS)/src

BUILD_DEPENDS = native/nodejs

HOMEPAGE = https://radarr.video/
COMMENT  = Radarr is a movie manager like Couchpotato, but based on the Sonarr codebase. It can monitor multiple RSS feeds for new movie releases and will grab, sorts and rename them. It can also be configured to automatically upgrade the quality of files already downloaded if a better quality format becomes available.
LICENSE  = GNU GPL v3

INSTALL_TARGET = radarr_install
DOTNET_OPTIMIZE = 1
DOTNET_OUTPUT_PATH = share
SET_VERSION = /p:AssemblyVersion=$(PKG_VERS) /p:FileVersion=$(PKG_VERS) /p:InformationalVersion=$(PKG_VERS) /p:Version=$(PKG_VERS)
DOTNET_BUILD_PROPERTIES += $(SET_VERSION)

include ../../mk/spksrc.cross-dotnet.mk

ENV += NPM_CONFIG_USER=root
PATH := $(WORK_DIR)/../../../native/nodejs/work-native/node/bin:$(PATH)

radarr_install:
	install -m 755 -d $(STAGING_INSTALL_PREFIX)/UI
	$(RUN) npm install && npm run build
	cp -R $(WORK_DIR)/$(PKG_NAME)-$(PKG_VERS)/_output/UI $(STAGING_INSTALL_PREFIX)/share/
