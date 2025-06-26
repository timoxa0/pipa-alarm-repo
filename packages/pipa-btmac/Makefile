PREFIX ?= /usr/local
BINDIR := $(PREFIX)/bin
LIBDIR := $(PREFIX)/lib

install-bin: pipa-btmac-set
	install -Dm755 pipa-btmac-set $(DESTDIR)$(BINDIR)/pipa-btmac-set

install-service: pipa-btmac.service
	install -Dm644 pipa-btmac.service $(DESTDIR)$(LIBDIR)/systemd/system/pipa-btmac.service

pipa-btmac.service: Makefile
	@echo "Generating systemd unit: $@"
	@echo "[Unit]" > $@
	@echo "Description=Set WLAN mac address based on board serial" >> $@
	@echo "Wants=network-pre.target" >> $@
	@echo "Before=network-pre.target" >> $@
	@echo "BindsTo=sys-subsystem-net-devices-wlan0.device" >> $@
	@echo "After=sys-subsystem-net-devices-wlan0.device" >> $@
	@echo "" >> $@
	@echo "[Service]" >> $@
	@echo "Type=oneshot" >> $@
	@echo "ExecStart=$(BINDIR)/pipa-btmac-set" >> $@
	@echo "" >> $@
	@echo "[Install]" >> $@
	@echo "WantedBy=multi-user.target" >> $@


install: install-bin install-service

.PHONY: install install-bin pipa-btmac.service
