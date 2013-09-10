BIN = ../bin
TST = ../tst
DAT = ../data
EXAMPLE = ../example

# for flex debugging, uncomment following line:
#DEBUG=-d

CXXFLAGS=-O2 -Wall

all: $(BIN) $(BIN)/hun_clean $(BIN)/hun_sentence $(BIN)/hun_abbrev $(BIN)/hun_abbrev_en $(BIN)/hun_sentclean $(BIN)/hun_token $(BIN)/hun_latin1 $(BIN)/hun_sentbreak

$(BIN):
	@mkdir $(BIN)

$(BIN)/hun_clean:  hun_clean.flex
	@echo compiling hun_clean
	-@flex $(DEBUG) hun_clean.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_clean
	@$(BIN)/hun_test $(BIN)/hun_clean hun_clean.flex

$(BIN)/hun_sentence: hun_sentence.flex
	@echo compiling hun_sentence
	-@flex $(DEBUG) hun_sentence.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_sentence
	@$(BIN)/hun_test $(BIN)/hun_sentence hun_sentence.flex

$(BIN)/hun_abbrev: __hun_abbrev.flex
	@echo compiling hun_abbrev
	-@flex $(DEBUG) __hun_abbrev.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_abbrev
	@$(BIN)/hun_test $(BIN)/hun_abbrev __hun_abbrev.flex

__hun_abbrev.flex: hun_abbrev.flex.m4 $(DAT)/abbrevations.txt
	@$(BIN)/hun_macro M4_MACRO_ABBREV $(DAT)/abbrevations.txt >__hun_abbrev.flex.m4
	@cat hun_abbrev.flex.m4 >>__hun_abbrev.flex.m4
	@cat __hun_abbrev.flex.m4 | m4 > __hun_abbrev.flex

$(BIN)/hun_abbrev_en: __hun_abbrev_en.flex
	-@flex $(DEBUG) __hun_abbrev_en.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_abbrev_en
	@$(BIN)/hun_test $(BIN)/hun_abbrev_en __hun_abbrev_en.flex

__hun_abbrev_en.flex: hun_abbrev_en.flex.m4 $(DAT)/abbrev_en.txt
	@$(BIN)/hun_macro M4_MACRO_ABBREV $(DAT)/abbrev_en.txt >__hun_abbrev_en.flex.m4
	@cat hun_abbrev_en.flex.m4 >>__hun_abbrev_en.flex.m4
	@cat __hun_abbrev_en.flex.m4 | m4 > __hun_abbrev_en.flex

$(BIN)/hun_sentclean: hun_sentclean.flex
	@echo compiling hun_sentclean
	-@flex $(DEBUG) hun_sentclean.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_sentclean
	@$(BIN)/hun_test $(BIN)/hun_sentclean hun_sentclean.flex

$(BIN)/hun_sentbreak: hun_sentbreak.flex
	@echo compiling hun_sentbreak
	-@flex $(DEBUG) hun_sentbreak.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_sentbreak
	@$(BIN)/hun_test $(BIN)/hun_sentence hun_sentbreak.flex

$(BIN)/hun_latin1: hun_latin1.flex
	@echo compiling hun_latin1
	-@flex $(DEBUG) hun_latin1.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_latin1

$(BIN)/hun_token: hun_token.flex
	@echo compiling hun_token
	-@flex $(DEBUG) hun_token.flex # -i -> ignore case, -f -8 fast
	@gcc $(CXXFLAGS) -lfl lex.yy.c -o $(BIN)/hun_token
	@$(BIN)/hun_test $(BIN)/hun_token hun_token.flex

#install:
#	@cp $(BIN)/huntoken $(BIN)/hun_head $(BIN)/hun_clean $(BIN)/hun_token $(BIN)/hun_abbrev \
	  $(BIN)/hun_abbrev_en $(BIN)/hun_sentclean $(BIN)/hun_sentbreak $(BIN)/hun_latin1 \
	  $(BIN)/hun_sentence $(BIN)
#	@test -d $(MAN)/man1 && cp man/huntoken.1 $(MAN)/man1 || echo "$(MAN)/man1 not exist"

#deinstall:
#	@test -f $(BIN)/huntoken && rm $(BIN)/huntoken || echo "$(BIN)/huntoken not exist"
#	@test -f $(BIN)/hun_head && rm $(BIN)/hun_head || echo "$(BIN)/hun_head not exist"
#	@test -f $(BIN)/hun_clean && rm $(BIN)/hun_clean || echo "$(BIN)/hun_clean not exist"
#	@test -f $(BIN)/hun_token && rm $(BIN)/hun_token || echo "$(BIN)/hun_token not exist"
#	@test -f $(BIN)/hun_abbrev && rm $(BIN)/hun_abbrev || echo "$(BIN)/hun_abbrev not exist"
#	@test -f $(BIN)/hun_abbrev_en && rm $(BIN)/hun_abbrev_en || echo "$(BIN)/hun_abbrev_en not exist"
#	@test -f $(BIN)/hun_sentclean && rm $(BIN)/hun_sentclean || echo "$(BIN)/hun_sentclean not exist"
#	@test -f $(BIN)/hun_sentbreak && rm $(BIN)/hun_sentbreak || echo "$(BIN)/hun_sentbreak not exist"
#	@test -f $(BIN)/hun_latin1 && rm $(BIN)/hun_latin1 || echo "$(BIN)/hun_latin1 not exist"
#	@test -f $(BIN)/hun_sentence && rm $(BIN)/hun_sentence || echo "$(BIN)/hun_sentence not exist"
#	@test -f $(MAN)/man1/huntoken.1 && rm $(MAN)/man1/huntoken.1 || echo "$(MAN)/man1/huntoken.1 not exist"
	
clean:
	@rm -f  *.o lex.yy.c
	@rm -f $(BIN)/hun_clean $(BIN)/hun_token $(BIN)/hun_abbrev $(BIN)/hun_abbrev_en \
	   $(BIN)/hun_sentclean $(BIN)/hun_latin1 $(BIN)/hun_sentence $(BIN)/hun_sentbreak
	@rm -f __*

test: $(BIN)/hun_*
	$(BIN)/huntoken <$(EXAMPLE)/HOLTLELKEK.txt >$(TST)/HOLTLELKEK.xml
	diff $(EXAMPLE)/HOLTLELKEK.xml $(TST)/HOLTLELKEK.xml
