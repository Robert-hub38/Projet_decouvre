######     SEGUNDA BITACORA DEL DIA 27/10/26  #####

##cOPIAR LOS ARCHIVOS DESCARGADOS AL DIRECTORIO INDICADO
cp ../../Téléchargements/en.txt.gz ../../Documents/EntreeSorties/

### DESCOMPRIMIR LOS ARCHIVOS 
gzip -dk en.txt.gz

### 
cat > comando-param-fr.txt << 'EOF'
# Comando utilizado para recrear el archivo param-fr
# Uso: cat fr.txt | wc -l >> param-fr
#      cat fr.txt | wc -w >> param-fr
#      cat fr.txt | wc -c >> param-fr
#
# Versión en una sola línea:
cat fr.txt | wc -l > param-fr && \
cat fr.txt | wc -w >> param-fr && \
cat fr.txt | wc -c >> param-fr
EOF

cat > comando-param.txt << 'EOF'
# Comando utilizado para recrear el archivo param-en     
# Uso: cat en.txt | wc -l >> param-en     
#      cat en.txt | wc -w >> param-en     
#      cat en.txt | wc -c >> param-en     
#
# Versión en una sola línea:
cat en.txt | wc -l > param-en && \
cat en.txt | wc -w >> param-en && \
cat en.txt | wc -c >> param-en
EOF



### DEUXIÈME PARTIE 
####### SEGUNDA PARTE #### 
####4.2 | Compter les occurrences des mots du fichier
#----------------------------------------------------------------------------------------------------
# Partie 4.2 : nettoyer le texte
cat fr.txt | sed -e 's/[[:punct:]]//g' -e 's/[0-9]//g' -e 's/./\L&/g' | grep -v '^$' > preproc_fr.txt
#----------------------------------------------------------------------------------------------------

#----------------------------------------------------------------------------------------------------
# Créer l'index global des mots
cat preproc_fr.txt | sed 's/ /\n/g' | grep -v '^$' | sort | uniq -c | sort -n > index_fr
#---------------------------------------------------------------------------------------------------

#---------------------------------------------------------------------------------------------------
# Créer le classement des 30 mots les plus utilisés
tail -n 30 index_fr | sort -nr > top_30_fr
#---------------------------------------------------------------------------------------------------

#---------------------------------------------------------------------------------------------------
# Créer le classement des 30 mots les moins utilisés
head -n 30 index_fr > last_30_fr
#---------------------------------------------------------------------------------------------------



