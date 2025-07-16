\# ============================================= \# COMANDOS PARA
ANÁLISIS FILOGENÉTICO DE RAG1 \# EN MUSTELIDAE \#
=============================================

\#
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\# 1. DESCARGAR SECUENCIAS DE NCBI (usando Entrez Direct) \#
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

\# Instalar Entrez Direct (solo primera vez) sh -c \"\$(curl -fsSL
ftp://ftp.ncbi.nlm.nih.gov/entrez/entrezdirect/install-edirect.sh)\"

esearch -db nucleotide -query \"Mustelidae\[Organism\] AND RAG1\[Gene\]
AND 3000:3500\[SLEN\]\" \| \\ efetch -format fasta \>
Mustelidae_RAG1.fasta

\#
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\# 2. ALINEAMIENTO MULTIPLE CON MUSCLE (PARÁMETROS OPTIMIZADOS) \#
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

muscle -in Mustelidae_RAG1_filtered.fasta -out
Mustelidae_RAG1_aligned.fasta

muscle -in Mustelidae_RAG1_filtered.fasta \\ -out
Mustelidae_RAG1_aligned.fasta \\ -maxiters 2 \\ -diags \\ -sv \\
-distance1 kbit20_3 \\ -cluster1 upgmb

\#
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--
\# 3. INFERENCIA FILOGENÉTICA CON IQ-TREE \#
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

iqtree -s Mustelidae_RAG1_aligned.fasta \\ -m MFP \\ -bb 1000 \\ -alrt
1000 \\ -nt AUTO \\ -pre Mustelidae_RAG1
