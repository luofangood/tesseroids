# Benchmark for calculating the effect of a tesseroid model
RESULT:=$(shell echo result-`tessgz --version`.txt)

run: $(RESULT)

model.txt:
	@echo "Generate the model"
	@../bin/tessgrd -r-10/10/-10/10 -b41/41 -z1000 | \
	../bin/tessmodgen -s0.5/0.5 -d2670 -z0 > model.txt

$(RESULT): model.txt
	@echo "Computer specs" > $@
	@cat /proc/cpuinfo | grep -m 1 -i -E 'model name' >> $@
	@cat /proc/meminfo | grep -m 1 -i -E 'MemTotal' >> $@
	@echo "\nTesseroids version\n" >> $@
	@tessgz --version >> $@
	@echo "" >> $@
	@../bin/tessgrd -r-8/8/-8/8 -b51/51 -z2000 > grid.txt
	@echo "\nModel size: `wc -l model.txt`" >> $@
	@echo "Grid size: `wc -l grid.txt`" >> $@
	@echo "Run the tesspot program"
	@echo "" >> $@
	@echo "Time spent on potential:" >> $@
	@/usr/bin/time -o $@ -a \
	../bin/tesspot model.txt -v < grid.txt > tmp.txt
	@echo ""
	@echo "Run the tessgz program"
	@echo "" >> $@
	@echo "Time spent on gz:" >> $@
	@/usr/bin/time -o $@ -a \
	../bin/tessgz model.txt -v < grid.txt > tmp.txt
	@echo ""
	@echo "Run the tessgzz program"
	@echo "" >> $@
	@echo "Time spent on gzz:" >> $@
	@/usr/bin/time -o $@ -a \
	../bin/tessgzz model.txt -v < grid.txt > tmp.txt
	@echo ""
	@echo "Results:"
	@cat $@

clean:
	rm -rf model.txt tmp.txt grid.txt
