ROOT:=			../..
COMMON_DIR:=		$(ROOT)/lightcrafts
include			$(COMMON_DIR)/mk/platform.mk

COMMON_PRODUCTS_DIR:=	$(COMMON_DIR)/products
COMMON_PRODUCTS:=	$(filter-out GNUmakefile,$(wildcard $(COMMON_PRODUCTS_DIR)/*))
DEST_COMMON_PRODUCTS:=	$(notdir $(COMMON_PRODUCTS))

MACOSX_LIB_DIR:=	../lib
MACOSX_LIBS:=		$(wildcard $(MACOSX_LIB_DIR)/*)
DEST_MACOSX_LIBS:=	$(notdir $(MACOSX_LIBS))

MACOSX_NIB_DIR:=	../resources/Resources/English.lproj
MACOSX_NIBS:=		$(wildcard $(MACOSX_NIB_DIR)/*.nib)
DEST_MACOSX_NIBS:=	$(notdir $(MACOSX_NIBS))

##
# Build rules
##

.PHONY: all

all: $(DEST_COMMON_PRODUCTS) $(DEST_MACOSX_LIBS) $(DEST_MACOSX_NIBS)

$(DEST_COMMON_PRODUCTS):
	$(call SYMLINK,$(COMMON_PRODUCTS_DIR)/$@,$@)

$(DEST_MACOSX_LIBS):
	$(call SYMLINK,$(MACOSX_LIB_DIR)/$@,$@)
	install_name_tool -change "/usr/local/opt/jpeg-turbo/lib/libjpeg.8.dylib" libjpeg.8.dylib libLCJPEG.jnilib
	install_name_tool -change "/usr/local/lib/libtiff.5.dylib" libtiff.5.dylib libLCTIFF.jnilib

$(DEST_MACOSX_NIBS):
	$(call SYMLINK,$(MACOSX_NIB_DIR)/$@,$@)

##
# Utility rules
##

.PHONY: clean distclean mostlyclean

clean distclean mostlyclean:
	$(RM) $(filter-out GNUmakefile,$(wildcard *))

# vim:set noet sw=8 ts=8:
