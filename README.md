#!/bin/sh
i=1
while [ $i == 1 ]
do
	echo "Iveskite failo varda:"
	read fv
	if [ -L $fv ]
	then
		echo "$fv tipas: simboline nuorodo, rodo i" '"'`readlink -f $fv`'"'
	elif [ -d $fv ]
	then
		echo "$fv tipas: katalogas, pakatalogiu skaicius jame" `ls -lR $fv | grep ^d | wc -l`
	elif [ -f $fv ]
	then
        	echo "$fv tipas: failas, kontroline suma" `cksum $fv | cut -f1`
	else
		echo "Tokio failo '$fv' nera"
		exit 1
	fi
done
