PREFIX ?= /usr/local
BINDIR := $(PREFIX)/bin
LIBDIR := $(PREFIX)/lib

install-bin: pipa-bt-mac-set
	install -Dm755 pipa-bt-mac-set $(DESTDIR)$(BINDIR)/pipa-bt-mac-set
	install -Dm755 pipa-wlan-mac-set $(DESTDIR)$(BINDIR)/pipa-wlan-mac-set

install-services: pipa-bt-mac.service pipa-wlan-mac.service
	install -Dm644 pipa-bt-mac.service $(DESTDIR)$(LIBDIR)/systemd/system/pipa-bt-mac.service
	install -Dm644 pipa-wlan-mac.service $(DESTDIR)$(LIBDIR)/systemd/system/pipa-wlan-mac.service

pipa-bt-mac.service: Makefile
	@echo "Generating systemd unit: $@"
	@echo "[Unit]" > $@
	@echo "Description=Set BT mac address" >> $@
	@echo "Wants=bluetooth.target" >> $@
	@echo "After=bluetooth.target" >> $@
	@echo "" >> $@
	@echo "[Service]" >> $@
	@echo "Type=oneshot" >> $@
	@echo "ExecStart=$(BINDIR)/pipa-bt-mac-set" >> $@
	@echo "RemainAfterExit=yes" >> $@
	@echo "TimeoutStartSec=10" >> $@
	@echo "" >> $@
	@echo "[Install]" >> $@
	@echo "WantedBy=multi-user.target" >> $@

pipa-wlan-mac.service: Makefile
	@echo "Generating systemd unit: $@"
	@echo "[Unit]" > $@
	@echo "Description=Set WLAN mac address based on board serial" >> $@
	@echo "Wants=network-pre.target" >> $@
	@echo "Before=network-pre.target" >> $@
	@echo "BindsTo=sys-subsystem-net-devices-wlp1s0.device" >> $@
	@echo "After=sys-subsystem-net-devices-wlp1s0.device" >> $@
	@echo "" >> $@
	@echo "[Service]" >> $@
	@echo "Type=oneshot" >> $@
	@echo "ExecStart=$(BINDIR)/pipa-wlan-mac-set" >> $@
	@echo "RemainAfterExit=yes" >> $@
	@echo "TimeoutStartSec=10" >> $@
	@echo "" >> $@
	@echo "[Install]" >> $@
	@echo "WantedBy=multi-user.target" >> $@

install: install-bin install-services

.PHONY: install install-bin pipa-bt-mac.service
