.PHONY: all maps conf mobxp mobxp-impl indent indent-items indent-mobs
# Can't be parallel due to the mobxp/indent-mobs conflict
.NOTPARALLEL:
all: maps conf
maps:
	ant -f tools/tmwcon/build.xml
	java -jar tools/tmwcon/converter.jar client-data/ world/map/
% : | %.example
	cp "$|" "$@"
conf: \
login/conf/login_local.conf login/conf/ladmin_local.conf login/save/gm_account.txt login/save/account.txt \
world/map/conf/map_local.conf world/map/conf/battle_local.conf world/map/conf/motd.txt world/map/conf/help.txt world/map/conf/atcommand_local.conf \
world/conf/char_local.conf

mobxp: mobxp-impl indent-mobs
mobxp-impl:
	mv world/map/db/mob_db.txt world/map/db/mob_db.old
	tools/mobxp < world/map/db/mob_db.old > world/map/db/mob_db.txt
	rm world/map/db/mob_db.old
indent: indent-mobs indent-items
indent-items: tools/aligncsv
	tools/aligncsv world/map/db/item_db.txt
indent-mobs: tools/aligncsv
	tools/aligncsv world/map/db/mob_db.txt
