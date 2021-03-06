NULL =

apidir = $(includedir)/gnome-settings-daemon-$(GSD_API_VERSION)/gnome-settings-daemon
api_DATA = gsd-enums.h

gsettings_ENUM_NAMESPACE = org.gnome.settings-daemon
gsettings_ENUM_FILES = $(top_srcdir)/data/$(api_DATA)

gsettings_SCHEMAS =							\
	org.gnome.settings-daemon.peripherals.gschema.xml		\
	org.gnome.settings-daemon.plugins.gschema.xml			\
	org.gnome.settings-daemon.plugins.keyboard.gschema.xml		\
	org.gnome.settings-daemon.plugins.power.gschema.xml		\
	org.gnome.settings-daemon.plugins.color.gschema.xml		\
	org.gnome.settings-daemon.plugins.media-keys.gschema.xml	\
	org.gnome.settings-daemon.plugins.xsettings.gschema.xml		\
	org.gnome.settings-daemon.plugins.housekeeping.gschema.xml	\
	org.gnome.settings-daemon.plugins.print-notifications.gschema.xml	\
	org.gnome.settings-daemon.peripherals.wacom.gschema.xml		\
	org.gnome.settings-daemon.plugins.xrandr.gschema.xml

all_schemas = $(gsettings_SCHEMAS)

if HAVE_PACKAGEKIT
gsettings_SCHEMAS += org.gnome.settings-daemon.plugins.updates.gschema.xml
else
all_schemas += org.gnome.settings-daemon.plugins.updates.gschema.xml
endif

if HAVE_GUDEV
gsettings_SCHEMAS += org.gnome.settings-daemon.plugins.orientation.gschema.xml
else
all_schemas += org.gnome.settings-daemon.plugins.orientation.gschema.xml
endif

@INTLTOOL_XML_NOMERGE_RULE@

@GSETTINGS_RULES@

convertdir = $(datadir)/GConf/gsettings
convert_DATA = gnome-settings-daemon.convert

@INTLTOOL_DESKTOP_RULE@
desktopdir = $(sysconfdir)/xdg/autostart
desktop_in_files = gnome-settings-daemon.desktop.in
desktop_DATA = $(desktop_in_files:.desktop.in=.desktop)

servicedir = $(datadir)/dbus-1/services
service_in_files = org.gnome.SettingsDaemon.service.in
service_DATA = $(service_in_files:.service.in=.service)

org.gnome.SettingsDaemon.service: org.gnome.SettingsDaemon.service.in Makefile
	$(AM_V_GEN) sed -e "s|\@libexecdir\@|$(libexecdir)|" $< > $@

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = gnome-settings-daemon.pc

@INTLTOOL_XML_NOMERGE_RULE@

man_MANS = gnome-settings-daemon.1

EXTRA_DIST = 					\
	$(man_MANS)				\
	$(convert_DATA)				\
	$(all_schemas:.xml=.xml.in.in)		\
	$(service_in_files)			\
	$(desktop_in_files)			\
	$(gsettings_ENUM_FILES)			\
	gnome-settings-daemon.pc.in		\
	$(api_DATA)				\
	$(NULL)

DISTCLEANFILES = 			\
	$(all_schemas)			\
	$(service_DATA)			\
	$(desktop_DATA)			\
	$(NULL)

MAINTAINERCLEANFILES =			\
	*~				\
	Makefile.in			\
	$(all_schemas:.xml=.valid)
