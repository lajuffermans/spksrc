SPK_NAME = dotnet-runtime
SPK_VERS = 6.0.12
SPK_REV = 3
SPK_ICON = src/dotnet.png

OPTIONAL_DEPENDS = cross/libstdc++
DEPENDS = cross/libicu cross/dotnet-runtime

UNSUPPORTED_ARCHS = $(DOTNET_UNSUPPORTED_ARCHS)

MAINTAINER = hgy59
DESCRIPTION = Free. Cross-platform. Open source. A developer platform for building all apps. This package installs the dotnet runtime and the asp.net.core runtime.
CHANGELOG = "1. Update to dotnet-runtime v6.0.12 (several security patches).<br/>2. Remove unsupported armv7 archs from provided packages."

STARTABLE = no
DISPLAY_NAME = .NET 6.0 runtime

HOMEPAGE = https://dotnet.microsoft.com/
LICENSE  = MIT

include ../../mk/spksrc.common.mk
ifeq ($(call version_lt, ${TCVERSION}, 7.0),1)
# we do not only need the updated libstdc++ library, we also need to
# adjust the library search path for dotnet to use this version.
DEPENDS += cross/libstdc++
POST_STRIP_TARGET = dotnet_patch_target
endif

SPK_COMMANDS = share/dotnet/dotnet

include ../../mk/spksrc.spk.mk

.PHONY: dotnet_patch_target
# Set library path to use bundled libstdc++
dotnet_patch_target:
	@$(MSG) "Set library runpath in dotnet executable."
	@patchelf --set-rpath /var/packages/$(SPK_NAME)/target/lib $(STAGING_DIR)/share/dotnet/dotnet
