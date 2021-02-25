ifndef CONFIG
  CONFIG=Release
endif

all: binary ttl_generator lv2

binary:
	$(MAKE) -f Makefile.binary CONFIG=$(CONFIG) DEBCXXFLAGS="$(DEBCXXFLAGS)" DEBLDFLAGS="$(DEBLDFLAGS)"

ttl_generator:
	$(MAKE) -f Makefile.ttl_generator CONFIG=$(CONFIG)

Vial.lv2: build/Vial.so lv2_ttl_generator
	mkdir -p Vial.lv2
	cp build/Vial.so Vial.lv2
	cd Vial.lv2 && ../lv2_ttl_generator ./Vial.so
	touch Vial.lv2

lv2: binary ttl_generator
	$(MAKE) Vial.lv2

clean:
	$(MAKE) clean CONFIG=$(CONFIG) -f Makefile.binary
	$(MAKE) clean CONFIG=$(CONFIG) -f Makefile.ttl_generator
	rm -rf build
	rm -rf Vial.lv2
