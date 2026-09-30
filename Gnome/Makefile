
# Makefile for Arch Linux ISO Build



.PHONY: all clean fix-label build



LABEL = NYARCH_GNOME



all: fix-label clean build



fix-label:

	@echo "==> Setting static volume label: $(LABEL)"

	@sed -i 's/iso_label=.*/iso_label="$(LABEL)"/g' profiledef.sh

	@find grub syslinux -type f \( -name "*.cfg" -o -name "*.lst" \) -exec sed -i 's/archisolabel=[^ ]*/archisolabel=$(LABEL)/g' {} +

	@find grub syslinux -type f \( -name "*.cfg" -o -name "*.lst" \) -exec sed -i 's/@ARCHISO_LABEL@/$(LABEL)/g' {} +

	@find grub/ -type f -name "*.cfg" -exec sed -i 's/vmlinuz-linux/vmlinuz-linux archisolabel=$(LABEL)/g' {} +

	@find grub/ -type f -name "*.cfg" -exec sed -i 's/archisolabel=$(LABEL) archisolabel=$(LABEL)/archisolabel=$(LABEL)/g' {} +



clean:

	@echo "==> Cleaning work/ and out/ directories..."

	@rm -rf work/ out/



build:

	@echo "==> Building custom Arch Linux ISO..."

	@chmod +x *.sh 2>/dev/null || true

	mkarchiso -v -w ./work -o ./out .

