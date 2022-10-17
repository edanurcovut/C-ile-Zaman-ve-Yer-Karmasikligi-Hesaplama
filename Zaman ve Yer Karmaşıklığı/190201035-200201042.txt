#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <time.h>

int main(void){

    /*
    sabitler => O(1)
    Logaritmik => O(logn)
    Lineer => O(n)
    Loglineer => O(n logn)
     Üstel => O(n^a) || O(a^n)
    */


    clock_t start, end;
    start = clock();
    //printf("Clock ticks at starting time: %ld\n", start);


    //Acilan dosya için kullanilacak pointer.
    FILE * dosya;

    //Okunacak verinin kaydedilecegi degisken.
    char * veri;
    char * verisuslua;
    char * verisusluk;

    //Dosyadan okunacak veri uzunlugu.
    int veri_uzunlugu=4000;
    int okunan=0;
    const char * dosya_adi="./ornek1.txt";

    //Dosya okumak için ikili modda aciliyor.
    dosya=fopen(dosya_adi,"r");

    //Dosyanin dogru sekilde acildigi kontrol ediliyor.
    if(dosya==NULL){
        printf("Dosya acilamadi.");
        return 0;
    }

    //Okunacak veri için bellekten yer ayriliyor.
    veri=(char *)malloc(veri_uzunlugu);
    verisuslua=(char *)malloc(veri_uzunlugu);
    verisusluk=(char *)malloc(veri_uzunlugu);
    //islemin dogrulugu kontrol ediliyor.
    if(veri==NULL){
        //Bellek hatasi.
        printf("Bellek hatasi olustu.\n");
        //Dosya kapatiliyor.
        fclose(dosya);
        //Programdan cikiliyor.
        return 0;
    }

    //Dosyadan veri okunuyor.
    okunan=fread(veri,1,veri_uzunlugu,dosya);
    // printf("%s dosyasindan %d bayt okundu.\n",dosya_adi,okunan);
    //okunan=fread(verisuslua,1,veri_uzunlugu,dosya);
    // printf("%s dosyasindan %d bayt okundu.\n",dosya_adi,okunan);
    //okunan=fread(verisusluk,1,veri_uzunlugu,dosya);
    // printf("%s dosyasindan %d bayt okundu.\n",dosya_adi,okunan);

    //Okunan verinin son bayti 0 degilse 0 yapiliyor.
    //Bu sayede string olarak sinirlandiriliyor.
    if(okunan>0){
        if(veri[okunan-1]!=0){
            veri[okunan-1]=0;
        }
        if(verisuslua[okunan-1]!=0){
            verisuslua[okunan-1]=0;
        }
        if(verisusluk[okunan-1]!=0){
            verisusluk[okunan-1]=0;
        }
    }



    //Okunan veri ekrana yazdiriliyor.
    //TODO: 2- Acilabilir kontrol amacli
    printf("\nOkunan kod parcacigi: \n%s\n",veri );
    //Bilgilendirme mesaji ekrana yazdiriliyor.
    //TODO: 2- Acilabilir Kontrol amacli

    //Dosya kapatiliyor.
    fclose(dosya);

    //Ayrilan bellek sisteme geri veriliyor.
    //free(veri);

    //

    char  blank[1000];
    char  karsilastirmadakiString[1000];
       int c = 0, d = 0;
       while (veri[c] != '\0')
       {
          if (veri[c] == '\n')
          {
             int temp = c + 1;
             if (veri[temp] != '\0')
             {
                while ((veri[temp] != ' ' || veri[c] == '\n') && veri[temp] != '\0')
                {
                   if ((veri[temp] == ' ' || veri[c] == '\n'))
                   {
                      c++;
                   }
                   temp++;
                }
             }
          }
          blank[d] = veri[c];
           karsilastirmadakiString[d] = veri[c];
          c++;
          d++;
          //printf("VERI %c",veri[c]);
       }

       blank[d] = '\0';
       karsilastirmadakiString[d] = '\0';
    //printf ("BLANK: \n\n%s", blank);
       //printf("\n%s\n", blank);

    	d = 0;
        //tüm yazilari LOWER cevir.
        int k = 0;
        while (blank[k]) {
            blank[k] = tolower(blank[k]);
            karsilastirmadakiString[k] = tolower(blank[k]);
            k++;
        }

        // ZAMAN KARMASİKLİGİ HESAPLA

        char zamanKarmasikligi[100] = " ";
        char *str = blank;

        //char *str ="ssasfodhjkasjdfor2131for1455";
        char *subtext = str;
        long nokVir, parantez= 0, parantezekadar;
        char arasi[1000];

        //FOR BULMADA HESAPLANAN DEÐERLER
        //---
        char *baslangic;
        long index1, gerikalan;
        //---

    int acikSusluParantez = 0, kapaliSusluParantez = 0;

    char *baslangicSusluAcik, *subtextSusluAcik = verisuslua;
    long index1SusluAcik, gerikalanSusluAcik;

    char *baslangicSusluKapali, *subtextSusluKapali = verisusluk;
    long index1SusluKapali, gerikalanSusluKapali;

    printf("----------------------------------\n");

    int hicForaGirdiMi = 0;

        //FORLARI HESAPLA
        int i = 0;
        int j = 0;
        for (i = 0; i<10; i++)
        {

            baslangic = strstr(str, "for");
            index1 = baslangic - str;
            gerikalan = strlen(str) - index1;
            //TODO: 2- Acilabilir kontrol amacli
            //printf("index1: %lo, gerikalan: %lo\n", index1, gerikalan);
            /*
            baslangic = strstr(subtext, "for");
            index1 = baslangic - subtext;
            gerikalan = strlen(subtext) - index1;
            */

            if(baslangic != NULL) //1 tane for buldu
            {
                hicForaGirdiMi++;
                //TODO: 2- Acilabilir kontrol amacli
                //printf("tamamý:    %s\n\n", blank);
                memcpy(subtextSusluAcik,&blank[0],index1);
                subtextSusluAcik[index1] = '\0';
                //TODO: 2- Acilabilir kontrol amacli
                //printf("FORA KADAR acik: %s\n\n", subtextSusluAcik);

                memcpy(subtextSusluKapali,&blank[0],index1);
                subtextSusluKapali[index1] = '\0';
                //TODO: 2- Acilabilir kontrol amacli
                //printf("FORA KADAR kapali: %s\n\n", subtextSusluKapali);

                memcpy(subtext,&subtext[index1+3],gerikalan);
                //TODO: 2- Acilabilir kontrol amacli
                //printf("%i. FOR: \n%s\n",i+1, subtext);





                //bulunan for'a kadar kac tane { kac tane } var

                acikSusluParantez = 0;
                kapaliSusluParantez=0;

                for (j = 0; j<10; j++)
                {
                    /*baslangic = strstr(subtext, ";");
                    nokVir = baslangic - subtext;
                    gerikalan = strlen(subtext) - nokVir;
                    memcpy(subtext,&subtext[nokVir+1],gerikalan);
                    */

                    baslangicSusluAcik = strstr(subtextSusluAcik, "{");
                    index1SusluAcik = baslangicSusluAcik - subtextSusluAcik;
                    gerikalanSusluAcik = strlen(subtextSusluAcik) - index1SusluAcik;
                    if(baslangicSusluAcik != NULL) //1 tane for buldu
                    {
                        memcpy(subtextSusluAcik,&subtextSusluAcik[index1SusluAcik + 1],gerikalanSusluAcik);
                        //printf("\n\n J=%i subtextSusluAcik-- : %s\n\n",j, subtextSusluAcik);
                        acikSusluParantez++;
                    }

                }
                //printf("\n\nacikSusluParantez: %i \n\n\n", acikSusluParantez);

                for (j = 0; j<10; j++)
                {
                    baslangicSusluKapali = strstr(subtextSusluKapali, "}");
                    index1SusluKapali = baslangicSusluKapali - subtextSusluKapali;
                    gerikalanSusluKapali = strlen(subtextSusluKapali) - index1SusluKapali;
                    if(baslangicSusluKapali != NULL) //1 tane for buldu
                    {
                        memcpy(subtextSusluKapali,&subtextSusluKapali[index1SusluKapali+1],gerikalanSusluKapali);
                        //printf("subtextSusluKapali-- %i: %s",j, subtextSusluAcik);
                        kapaliSusluParantez++;
                    }
                }
                if(acikSusluParantez == (kapaliSusluParantez+1) ) //fonksiyonunki de var
                {
                    if(i == 0)
                        strcat(zamanKarmasikligi,"+");
                    else
                    strcat(zamanKarmasikligi,"*");
                }
                else
                {
                    strcat(zamanKarmasikligi,"+");
                    //TODO: Acilabilir kontrol amacli
                    //printf("acikSusluParantez: %i, kapaliSusluParantez: %i\n", acikSusluParantez, kapaliSusluParantez);
                }
                //BULUNAN FOR ICINDEKI KARMASIKLIK:

                /*                              */

                // for'un içindeki karmasikligi hesapla

                // ikinci noktali virgül ve parantez arasina gir.
                //birinci
                baslangic = strstr(subtext, ";");
                nokVir = baslangic - subtext;
                gerikalan = strlen(subtext) - nokVir;
                memcpy(subtext,&subtext[nokVir+1],gerikalan);
                //TODO: Acilabilir Kontrol amacli
                //printf("ILK IFADE: \n%s\n", subtext);
                //ikinci
                baslangic = strstr(subtext, ";");
                nokVir = baslangic - subtext;
                gerikalan = strlen(subtext) - nokVir;
                memcpy(subtext,&subtext[nokVir+1],gerikalan);
                //TODO: Acilabilir kontrol amacli
                //TODO: 2- Acilabilir kontrol amacli
                //printf("IKINCCI IFADE: \n%s\n", subtext);
                //ÝFADE
                if(baslangic != NULL) //for varsa
                {
                    baslangic = strstr(subtext, ")");
                    parantez = baslangic - subtext;
                    parantezekadar = strlen(subtext) - parantez;
                    if(baslangic != NULL) //for varsa
                    {
                        memcpy(arasi,&subtext[0],gerikalan-parantezekadar-1); //1 tane for buldu
                        //TODO: Acilabilir kontrol amacli
                        //printf("ARADAKI IFADE: \n%s\n", arasi);
                        if(strstr(arasi, "*") != NULL)
                            strcat(zamanKarmasikligi,"logn");
                        else if(strstr(arasi, "/") != NULL)
                            strcat(zamanKarmasikligi,"logn");
                        else if(strstr(arasi, "+") != NULL)
                            strcat(zamanKarmasikligi,"n");
                        else if(strstr(arasi, "-") != NULL)
                            strcat(zamanKarmasikligi,"n");
                    }
                }
            }
            else
            {
                break;
            }
        }

    //hiC for yoksa
    if(hicForaGirdiMi == 0)
        strcat(zamanKarmasikligi,"?");


    //WHILE HESAPLA
    //kac tane while var bulalim

    char wh[5] = "while";
    int flag=0;
    int bulunanWhile=0;
    int whIndex[5];
    for(i = 0; i< 1000; i++)
    {
        flag = 0;
        for(j=0; j<5; j++)
        {
            if(karsilastirmadakiString[i+j] == wh[j])
            {
                flag=flag+1;
                if(flag == 5)
                {
                    whIndex[bulunanWhile] = i;
                    bulunanWhile++;

                }
            }
        }

    }
    //while sayisi bulundu.
    //simdi whileden önce ve sonra 10 karakterde +,-,*,/ var mi bakalim.

    //oncesine ve sonrasinda ayni anda bakiliyor
    int bulunduMu = 0;
    for(k=0; k<bulunanWhile; k++)
    {
        for(i=0; i<10; i++)
        {
            //oncesi
            if(karsilastirmadakiString[whIndex[k]-i] == '+')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+"); //bulunan her while sonrasi big O'da + yazdirmak
                strcat(zamanKarmasikligi,"n");
                bulunduMu++;
                break;
            }
            else if(karsilastirmadakiString[whIndex[k]-i] == '-')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+");
                strcat(zamanKarmasikligi,"n");
                bulunduMu++;
                break;
            }
            else if(karsilastirmadakiString[whIndex[k]-i] == '*')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+");
                strcat(zamanKarmasikligi,"logn");
                bulunduMu++;
                break;
            }
            else if(karsilastirmadakiString[whIndex[k]-i] == '\\')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+");
                strcat(zamanKarmasikligi,"logn");
                bulunduMu++;
                break;
            }
            //sonrasi
            if(karsilastirmadakiString[whIndex[k]+i] == '+')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+");
                strcat(zamanKarmasikligi,"n");
                bulunduMu++;
                break;
            }
            else if(karsilastirmadakiString[whIndex[k]+i] == '-')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+");
                strcat(zamanKarmasikligi,"n");
                bulunduMu++;
                break;
            }
            else if(karsilastirmadakiString[whIndex[k]+i] == '*')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+");
                strcat(zamanKarmasikligi,"logn");
                bulunduMu++;
                break;
            }
            else if(karsilastirmadakiString[whIndex[k]+i] == '\\')
            {
                if(bulunduMu != 0)
                    strcat(zamanKarmasikligi,"+"); //bulunan her while sonrasi big O'da + yazdirmak
                strcat(zamanKarmasikligi,"logn");
                bulunduMu++;
                break;
            }
        }



    }

    //recursive kontrolü
    //returndeki deger ;'e kadar alinie bosluktan öncesi ve sonrasi seklinde buradaki degerler bir diziye atiliyor.

    char returnDegerleri [10][100];
    int returndekiDegerler = 0;
    char rt[6] = "return";
    for(i = 0; i< 1000; i++)
    {
        flag = 0;
        for(j=0; j<6; j++)
        {
            if(karsilastirmadakiString[i+j] == rt[j])
            {
                flag=flag+1;
                if(flag == 6)
                {
                    //return buldu

                    //bosluk ya da ; bulana kadar devam
                    for(k=0; k<150; k++)
                    {
                        if(karsilastirmadakiString[i+j+k] != ';')
                        {
                            if(karsilastirmadakiString[i+j+k+1] != ';')
                             returnDegerleri[returndekiDegerler][k] = karsilastirmadakiString[i+j+k+1];
                            else
                                returnDegerleri[returndekiDegerler][k] = '\0';
                        }
                        else if(karsilastirmadakiString[i+j+k] == ';')
                        {
                            break;
                        }
                        else
                        {
                            k++;
                        }
                    }
                    returndekiDegerler++;
                }
            }
        }

    }

    /*
    printf("KAÇ RETURN VAR:%i", returndekiDegerler);
    printf("\nRETURN 1:%s", returnDegerleri[0]);
    printf("\nRETURN 2:%s", returnDegerleri[1]);
    printf("\nRETURN 3:%s", returnDegerleri[2]);
    */

    int bulunanRecReturn = 0;

    //bu degerlerde fonksiyon var mi bakilyor (icerisinde kaç tane parantez varsa o kadar fonksiyon cagirilmasi vardir.)

    for(i=0; i<returndekiDegerler; i++)
    {
        for(j=0; j<150; j++)
        {
            if(returnDegerleri[i][j] == '(')
            {
                if(bulunanRecReturn > 0)
                    strcat(zamanKarmasikligi,"+n");
                else
                    strcat(zamanKarmasikligi,"n");
                bulunanRecReturn++;
            }
            if(returnDegerleri[i][j] == '\0')
                break;
        }
    }



    //recursive kontrolu de girince
    if(hicForaGirdiMi == 0 && bulunanWhile == 0 && bulunanRecReturn == 0)
        strcat(zamanKarmasikligi,"1");





    //TOPLAM BIG(O)
    //printf("\n\nZaman Karmasikligi:   O(%s)",zamanKarmasikligi );
    printf("\n\nToplam Zaman Karmasikligi:   O(");
    k = 2;
    while (zamanKarmasikligi[k]) {
        printf("%c", zamanKarmasikligi[k]);
        k++;
    }
    printf(")\n");




    //YER KARMASİKLİGİ HESAPLA

    //sirayla tanımlamalara bakiliyor
    // ; varsa arada , var mi aranyor. varsa +1 ile deger çarpiliyor yoksa deger yaziliyor.
    //en son -varsa- return degeri de eklenir.

    // sadece RAM'de 1 ve 4 byte yer kaplayan degerleri açtik digerleri de acilip copy paste yapilabilir.
    char *birlik   [4]  = { "bool ","char ","unsigned char ","__int8 "};
    //char *ikilik   [3]  = { "__int16 ","short ", "unsigned short "};
    char *dortluk  [5]  = { "float ","int ","long ","unsigned int ","__int32 " };
    //char *sekizlik [4]  = { "double ","__int64 ","long double ","long long "};

    //birlik
    int toplamYer1 = 0;
    int toplamYer1N = 0;
    int nVarMi1=0;
    char birlikler [1000];
    int ch = 0;
    int s = 0;
    for(s=0; s<4; s++)
    {
        for(i = 0; i< 1000; i++)
        {
            flag = 0;
            for(j=0; j<6; j++)
            {
                if(karsilastirmadakiString[i+j] == birlik[s][j])
                {
                    flag=flag+1;
                    if(flag == strlen(birlik[s]))
                    {
                        //return buldu

                        //bosluk ya da ; bulana kadar devam
                        for(k=0; k<150; k++)
                        {
                            if(karsilastirmadakiString[i+j+k] != ';')
                            {
                                if(karsilastirmadakiString[i+j+k+1] != ';')
                                {
                                    birlikler[ch] = karsilastirmadakiString[i+j+k];
                                    ch++;
                                }
                                else
                                    birlikler[ch] = '\0';
                            }
                            else if(karsilastirmadakiString[i+j+k] == ';')
                            {
                                break;
                            }
                            else
                            {
                                k++;
                            }
                        }
                        birlikler[ch] = '|';
                        for(d=0; d<strlen(birlikler); d++)
                        {
                            if(birlikler[d] == '[')
                            {
                                toplamYer1N++;
                                nVarMi1 = 1;
                            }
                        }
                        ch = 0;
                        if(nVarMi1 == 0)
                            toplamYer1++;
                        nVarMi1 = 0;
                    }
                }
            }

        }
    }
    //dortluk
    int toplamYer4 = 0;
    int toplamYer4N = 0;
    int nVarMi=0;
    char dortlukler [1000];
    ch = 0;
    for(s=0; s<5; s++)
    {
        for(i = 0; i< 1000; i++)
        {
            flag = 0;
            for(j=0; j<6; j++)
            {
                if(karsilastirmadakiString[i+j] == dortluk[s][j])
                {
                    flag=flag+1;
                    if(flag == strlen(dortluk[s]))
                    {
                        //return buldu

                        //bosluk ya da ; bulana kadar devam
                        for(k=0; k<150; k++)
                        {
                            if(karsilastirmadakiString[i+j+k] != ';')
                            {
                                if(karsilastirmadakiString[i+j+k+1] != ';')
                                {
                                    dortlukler[ch] = karsilastirmadakiString[i+j+k];
                                    ch++;
                                }
                                else
                                    dortlukler[ch] = '\0';
                            }
                            else if(karsilastirmadakiString[i+j+k] == ';')
                            {
                                break;
                            }
                            else
                            {
                                k++;
                            }
                        }
                        dortlukler[ch] = '|';
                        for(d=0; d<strlen(dortlukler); d++)
                        {
                            if(dortlukler[d] == '[')
                            {
                                toplamYer4N++;
                                nVarMi = 1;
                            }
                        }
                        ch = 0;
                        if(nVarMi == 0)
                            toplamYer4++;
                        nVarMi = 0;
                    }
                }
            }

        }
    }

    //printf("\ndortluk sayisi:n: %i\n" , toplamYer4N);
    //printf("\ndortluk sayisi:: %i\n" , toplamYer4);
    //printf("dortlukler: %s", dortlukler);
    if((toplamYer4N*4) + (toplamYer1N*1) > 0 && (toplamYer4*4) + (toplamYer1*1) > 0 )
        printf("Toplam yer karmasikligi  :   %in + %i\n", (toplamYer4N*4) + (toplamYer1N*1) , (toplamYer4*4) + (toplamYer1*1)  );
    else if((toplamYer4N*4) + (toplamYer1N*1) > 0 && (toplamYer4*4) + (toplamYer1*1) <= 0)
        printf("Toplam yer karmasikligi  :   %in \n", (toplamYer4N*4) + (toplamYer1N*1)   );
    else if((toplamYer4N*4) + (toplamYer1N*1) <= 0 && (toplamYer4*4) + (toplamYer1*1) > 0 )
        printf("Toplam yer karmasikligi  :   %i\n", (toplamYer4*4) + (toplamYer1*1)  );
    else
        printf("Toplam yer karmasikligi  :   %in + %i\n", (toplamYer4N*4) + (toplamYer1N*1) , (toplamYer4*4) + (toplamYer1*1)  );

    end = clock();
    //printf("Clock ticks at end time: %ld\n", end);
    //printf("CLOCKS_PER_SEC: %i\n", CLOCKS_PER_SEC);
    printf("Gecen sure               :   %f ms \n\n\n", (float)(end-start)/CLOCKS_PER_SEC);


    //Programdan cikiliyor.
    return 0;

}

