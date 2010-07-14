# 
# kyak@freenode/#qi-hardware
#
# This is free software, licensed under the GNU General Public License v2.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=jfbterm
PKG_VERSION:=0.4.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://jaist.dl.sourceforge.jp/jfbterm/13501/
PKG_MD5SUM:=cb0b869bd1c21f0dd224b7fc40517680

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/jfbterm
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=J framebuffer terminal / Multilingual Enhancement
  URL:=http://jfbterm.sourceforge.jp
  SUBMENU:=terminal
  DEPENDS:=libiconv
endef

define Package/jfbterm/description
  JFBTERM takes advantages of framebuffer device and makes it
  able to display multilingual text on console.
endef

TARGET_CFLAGS+= \
       -I$(STAGING_DIR)/usr/lib/libiconv/include \
       -I$(LINUX_DIR)/include

TARGET_LDFLAGS+= \
        -Wl,-rpath-link=$(STAGING_DIR)/usr/lib \
        -L$(STAGING_DIR)/usr/lib/libiconv/lib -liconv

MAKE_FLAGS += ACLOCAL=aclocal-1.10 AUTOMAKE="automake-1.10 -a"

#CONFIGURE_VARS += ac_cv_func_ioperm=no

#CONFIGURE_ARGS += \
	--enable-vga16fb=no

#TARGET_CFLAGS += -Wall -g

#define Build/Configure
#	$(call Build/Configure/Default, \
		--enable-vga16fb=no, \
		ac_cv_func_ioperm=no)
#endef

define Package/jfbterm/install
	$(INSTALL_DIR) \
		$(1)/usr/bin \
		$(1)/etc \
		$(1)/usr/share/fonts/jfbterm \
		$(1)/usr/share/terminfo/j

	$(INSTALL_BIN) \
		$(PKG_BUILD_DIR)/jfbterm \
		$(1)/usr/bin/jfbterm

	$(INSTALL_DATA) \
		./config/jfbterm.conf \
		$(1)/etc/jfbterm.conf

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/fonts/* \
		$(1)/usr/share/fonts/jfbterm

	$(INSTALL_DATA) \
		./fonts/* \
		$(1)/usr/share/fonts/jfbterm

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/terminfo.jfbterm \
		$(1)/usr/share/terminfo/j/jfbterm

endef

$(eval $(call BuildPackage,jfbterm))