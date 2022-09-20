include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=qca-nss-fw-hk
PKG_BRANCH:=nss
PKG_VERSION:=020
PKG_RELEASE:=1
PKG_MD5SUM:=skip

NSS_VER:=12.0
NSS_SOC:=HK
NSS_PROFILE:=R

PKG_SOURCE:=BIN-NSS.FW.12.0.r1-002-HK.R.tar.bz2
PKG_SOURCE_URL:=https://github.com/quic/qca-sdk-nss-fw/blob/main/QCA_Networking.SPF_11.5.0/CS/IPQ8074.ATH.11.5.0/BIN-NSS.FW.12.0.r1-002-HK.R.tar.bz2?raw=true
PKG_BUILD_DIR:=$(BUILD_DIR)/BIN-NSS.FW.12.0.r1-002-HK.R

include $(INCLUDE_DIR)/package.mk

define NssFirmware

  define Package/$(PKG_NAME)-$(1)
    SECTION:=kernel
    CATEGORY:=$(QTI_SOFTWARE_CATEGORY)
    SUBMENU:=Network Devices
    DEPENDS:=@TARGET_ipq_ipq807x||TARGET_ipq_ipq807x_64||TARGET_ipq807x_32||TARGET_ipq807x
    TITLE:=NSS firmware binaries - $(1)
    PROVIDES:=$(PKG_NAME)
    MENU:=1
  endef

  define Package/$(PKG_NAME)-$(1)/description
  This package contains the NSS firmwares ($(1)) for QTI chipset
  endef

  define Package/$(PKG_NAME)-$(1)/install
	$(INSTALL_DIR) $$(1)/lib/firmware/qca
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/$(2)0.bin $$(1)/lib/firmware/qca-nss0-$(1).bin
  ifneq ($(CONFIG_KERNEL_IPQ_MEM_PROFILE),256)
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/$(2)1.bin $$(1)/lib/firmware/qca-nss1-$(1).bin
  endif
  endef
  $$(eval $$(call BuildPackage,$(PKG_NAME)-$(1)))
endef

Build/Compile=true

$(eval $(call NssFirmware,retail,retail_router))
