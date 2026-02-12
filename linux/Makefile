TARGET_SYMBOLS := /usr/share/X11/xkb/symbols/us
SOURCE_SYMBOLS := usr-share-X11-xkb-symbols-us
TARGET_RULES := /usr/share/X11/xkb/rules/evdev.xml
SOURCE_RULES := usr-share-X11-xkb-rules-evdev
TARGET_USER ?= $(SUDO_USER)
TARGET_COMPOSE := $(shell getent passwd $(TARGET_USER) | cut -d: -f6)/.XCompose
SOURCE_COMPOSE := XCompose

all: reinstall

install: $(SOURCE_SYMBOLS) $(TARGET_SYMBOLS) $(SOURCE_RULES) $(TARGET_RULES)
	cat $(SOURCE_SYMBOLS) >> $(TARGET_SYMBOLS)
	sed -i "$$(awk '/variantList/{ print NR; exit }' $(TARGET_RULES)) r $(SOURCE_RULES)" $(TARGET_RULES)
	install -o $(TARGET_USER) -g $(TARGET_USER) $(SOURCE_COMPOSE) $(TARGET_COMPOSE)

uninstall: $(TARGET_SYMBOLS) $(TARGET_RULES)
	sed -i '/ ENGRAMMER BEGIN /,/ ENGRAMMER END /d' $^
	mv $(TARGET_COMPOSE) $(TARGET_COMPOSE).bak

reinstall:
	$(MAKE) uninstall
	$(MAKE) install

.PHONY: all install uninstall reinstall
