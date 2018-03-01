# Uputstvo-za-OTA


Uputstvo za implementaciju OTA u vec postojeci projekat bez OTA.

1. Prekopirati folder "components" u folder radnog projekta.

2. Ako u radnom main folderu nema Kconfig fajla, prekopirati Kconfig iz menu foldera OTA templejt-a. 
	U suprotnom, ako u radnom main folderu ima Kconfig onda prekopirati konfiguracije za WIFI_SSID i WIFI_PASSWORD. 
	Ako vec postoje konfiguracije ne kopirati nista.
	
3. Iz main.c OTA templejt-a prekopirati sve sto nema u radnom projektu, #include , metode, funkcije i taskove. 
	Ali ne kopirati npr ako ima vec inicijalizovan wifi ili error hendler, vec samo ono sto se razlikuje 
	inace ce doci do problema pa ce esp da se resetuje stalno.


4. U mingw32 kucati make menuconfig, i podesiti wifi i password. U menuconfig takodje
	podesiti Partition Table na Factory app, two OTA definitions. Sacuvati sve izmene.
	
5. U mingw32 kucati make erase_flash flash monitor i ako je sve uspesno 
	trebala bi da pise ip adresa modula koja se posle kuca za upload koda.
	
6. U Makefile radnog projekta dodati 

	ota: app
	curl ${ESP32_IP}:8032 --data-binary @- < build/$(PROJECT_NAME).bin

	po uzoru na makefile iz templejta. 
 
7. U mingw32 kucati make ota ESP32_IP=192.168.0.29 (ip adresu izmeniti na pravu, ovo je samo primer).
	
	Ako je sve uspesno, pisace Success. Next boot partition is ota_0. 
	ota_0 i ota_1 se menjaju pri upisu naizmenicno jer trenutni firmver se ne zaustavlja
	 dok se novi firmver skroz ne upise,
	i onda ga bootloader uputi da je novi firmver na drugoj particiji.
	
Posoliti po zelji. Prijatno!
 



	

	