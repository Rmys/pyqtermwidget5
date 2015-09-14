TARGET = QTermWidget.so
OFILES = sipQTermWidgetcmodule.o sipQTermWidgetQTermWidget.o
HFILES = sipAPIQTermWidget.h 

CC = gcc
CXX = g++
LINK = g++
CPPFLAGS = -DNDEBUG -I. -I/usr/include/qt5 -I/usr/include/qt5/QtCore -I/usr/include/qt5/QtGui -I/usr/include/qt5/QtWidgets -I/usr/include/python2.7
CFLAGS = -pipe -mtune=generic -march=x86-64 -O2 -pipe -fstack-protector -D_FORTIFY_SOURCE=2 -g -fPIC -fPIC -O2 -Wall -W
CXXFLAGS = -pipe -mtune=generic -march=x86-64 -O2 -pipe -fstack-protector -D_FORTIFY_SOURCE=2 -g -fPIC -fPIC -O2 -Wall -W
LFLAGS = -shared -lpython2.7 -Wl,--version-script=QTermWidget.exp
LIBS = -L.. -lqtermwidget5 -lQt5Core -lQt5Gui -lQt5Widgets
.SUFFIXES: .c .o .cpp .cc .cxx .C


.cpp.o:
	$(CXX) -c $(CXXFLAGS) $(CPPFLAGS) -o $@ $<

.cc.o:
	$(CXX) -c $(CXXFLAGS) $(CPPFLAGS) -o $@ $<

.cxx.o:
	$(CXX) -c $(CXXFLAGS) $(CPPFLAGS) -o $@ $<

.C.o:
	$(CXX) -c $(CXXFLAGS) $(CPPFLAGS) -o $@ $<

.c.o:
	$(CC) -c $(CFLAGS) $(CPPFLAGS) -o $@ $<

all: $(TARGET)

$(OFILES): $(HFILES)

$(TARGET): $(OFILES)
	@echo '{ global: initQTermWidget; local: *; };' > QTermWidget.exp
	$(LINK) $(LFLAGS) -o $(TARGET) $(OFILES) $(LIBS)

install: $(TARGET)
	@test -d $(DESTDIR)/usr/lib/python2.7/site-packages || mkdir -p $(DESTDIR)/usr/lib/python2.7/site-packages
	cp -f $(TARGET) $(DESTDIR)/usr/lib/python2.7/site-packages/$(TARGET)
	@test -d $(DESTDIR)/usr/share/sip/qtermwidget5 || mkdir -p $(DESTDIR)/usr/share/sip/qtermwidget5
	cp -f qtermwidget.sip $(DESTDIR)/usr/share/sip/qtermwidget5/qtermwidget.sip
	@test -d $(DESTDIR)/usr/lib/python2.7/site-packages || mkdir -p $(DESTDIR)/usr/lib/python2.7/site-packages
	cp -f qtermwidgetconfig.py $(DESTDIR)/usr/lib/python2.7/site-packages/qtermwidgetconfig.py

clean:
	-rm -f $(TARGET)
	-rm -f sipQTermWidgetcmodule.o
	-rm -f sipQTermWidgetQTermWidget.o
	-rm -f QTermWidget.exp
