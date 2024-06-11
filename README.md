# Documentation_KAI

Extract PDF :

```mermaid
flowchart  TD;
A[PDF]--PDF file -->B[Check Type];
B-- Scan PDF?-->C[Extract Scan PDF];
B-- PDF file-->C;
B-- PDF file-->D;
B-- Real PDF?-->D[Extract Real PDF];
C-- List -->F[Assembler Block];
D-- List -->F;
F-- List -->G[Final Result];
```

```mermaid
flowchart  TD;
A[PDF]-- PDF file -->B[Check Type];
B-- Scan PDF?-->C[Extract Scan PDF];
B-- PDF file-->C;
C-- PDF Base 64 -->Dd[PDF to IMG];
Dd-- Images --> Ee[Segmentation];
Ee-- Text Image Blocks -->Ff[OCR Text];
Ee-- Table Image Blocks -->Gg[OCR Table];
Ee-- Figure Image Blocks -->Hh[OCR Figure];
Ff-- String -->Ii[Correction];
Ii-- String -->Jj[Result];
Gg-- String -->Jj;
Hh-- String -->Jj;
B-- PDF file-->D;
B-- Real PDF?-->D[Extract Real PDF];
D-- PDF file -->K[Handle One Page];
K-- PDF Base 64 -->L[PDF to IMG];
L-- Image -->M[Segmentation];
M-- Graph ?-->N[OCR];
M-- Images Blocks -->N;
M-- Page + Images Blocks -->O;
M-- No Graph?-->O[Extract Real PDF];
N-- Text Image Blocks -->P[OCR Text];
N-- Table Image Blocks -->Q[OCR Table];
N-- Figure Image Blocks -->R[OCR Figure];
P-- String -->S[Correction];
S-- String -->T[Result];
Q-- String -->T;
R-- String -->T;
O-- Page -->U[Extract Text];
O-- Table Image Blocks -->V[OCR Table];
O-- Figure Image Blocks -->X[OCR Figure];
U-- String -->W[Remove Line Break];
W-- String -->Y[Result];
V-- String -->Y;
X-- String -->Y;
T-- List -->Z[Final Result Real PDF];
Y-- List -->Z;
Jj-- List -->Fa[Assembler Block];
Z-- List -->Fa;
Fa-- List -->Ga[Final Result];
```


Extract real pdf : 

```mermaid
flowchart  TD;
A[PDF + List Page]-- PDF file -->B[Handle One Page];
B-- PDF Base 64 -->C[PDF to IMG];
C-- Image -->D[Segmentation];
D-- Graph ?-->E[OCR];
D-- Images Blocks -->E
D-- Page + Images Blocks -->F
D-- No Graph?-->F[Extract Real PDF];
E-- Text Image Blocks -->G[OCR Text];
E-- Table Image Blocks -->H[OCR Table];
E-- Figure Image Blocks -->I[OCR Figure];
G-- String -->M[Correction];
M-- String -->P[Result];
H-- String -->P;
I-- String -->P;
F-- Page -->J[Extract Text];
F-- Table Image Blocks -->K[OCR Table];
F-- Figure Image Blocks -->L[OCR Figure];
F-- Image detected by PymuPDF -->L[OCR Figure];
J-- String -->N[Remove Line Break];
N-- String -->Q[Result];
K-- String -->Q;
L-- String -->Q;
P-- List -->R[Final Result Real PDF];
Q-- List -->R;
```

Extract Scan PDF:

```mermaid
flowchart  TD;
A[PDF + List Page]-- PDF Base 64 -->B[PDF to IMG];
B-- Images --> C[Segmentation];
C-- Text Image Blocks -->G[OCR Text];
C-- Table Image Blocks -->H[OCR Table];
C-- Figure Image Blocks -->I[OCR Figure];
G-- String -->J[Correction];
J-- String -->K[Result];
H-- String -->K;
I-- String -->K;
```

Word:

```mermaid
flowchart TD;
A[WORD file]-- DOCX ? -->B[ Extract from DOCX];
A-- DOC ? -->C[Extract from DOC];
B-->D[Text];
B-->I[Table];
B-->E[Figure];
B-->G[Graph];
B-->H[Smart Art];
B-->F[Catalog];
I-->J[CSV Interpreter];
E-->K[OCR Figure];
G-->J;
D-->L[Result];
J-->L;
H-->L;
F-->L;
K-->L;
L--Error ? -->M[Extract PDF];
L--No Error ? -->N[Final Result];
C-->M;
M-->N
```


PowerPoint:

```mermaid
flowchart TD;
A[PPTX file]-->B[Extract from PPTX];
B-->C[Extract One Slide];
C-->D[Extract different type];
D-->E[Placeholder];
E-->F;
E-->G;
D-->F[Text];
D-->G[Image];
D-->H[Table];
D-->I[Chart];
D-->J[Smart Art];
G-->K[OCR Figure];
F-->L[Recompose Slide];
K-->L;
H-->L;
I-->L;
J-->L;
L-->M[Result for one slide];
M-->N[Final result]
```

Excel:

```mermaid
flowchart TD;
Aex[Excel file]-->Bex[Extract Excel];
Bex --> Cex[Sheet CSV];
Cex-- <= Max Token --> Dex[CSV Interpreter];
Dex-->Eex[Result];
Cex-- >= Max Token -->Fex[Split with token];
Fex-->Dex;
Cex-- Image ? --> Gex[OCR Figure];
Gex-->Eex
```



All : 

```mermaid
flowchart TD;
A[File] -- PDF --> B[Extract PDF];
B[PDF]-->Bpdf[Check Type];
Bpdf-- Scan PDF-->Cpdf[Extract Scan PDF];
Cpdf -->Ddpdf[pdfPDF to IMG];
Ddpdf--> Eepdf[Segmentation];
Eepdf-->Ffpdf[OCR Text];
Eepdf -->Ggpdf[OCR Table];
Eepdf -->Hhpdf[OCR Figure];
Ffpdf-->Iipdf[Correction];
Iipdf -->Jjpdf[Result];
Ggpdf -->Jjpdf;
Hhpdf -->Jjpdf;
Bpdf-- Real PDF -->Dpdf[Extract Real PDF];
Dpdf-->Kpdf[Handle One Page];
Kpdf -->Lpdf[PDF to IMG];
Lpdf -->Mpdf[Segmentation];
Mpdf--Graph -->Npdf[OCR];
Mpdf--No Graph-->Opdf[Extract Real PDF];
Npdf -->Ppdf[OCR Text];
Npdf -->Qpdf[OCR Table];
Npdf -->Rpdf[OCR Figure];
Ppdf -->Spdf[Correction];
Spdf -->Tpdf[Result];
Qpdf -->Tpdf;
Rpdf -->Tpdf;
Opdf -->Updf[Extract Text];
Opdf -->Vpdf[OCR Table];
Opdf -->Xpdf[OCR Figure];
Updf -->Wpdf[Remove Line Break];
Wpdf -->Ypdf[Result];
Vpdf -->Ypdf;
Xpdf -->Ypdf;
Tpdf -->Zpdf[Final Result Real PDF];
Ypdf -->Zpdf;
Jjpdf -->Fapdf[Assembler Block];
Zpdf -->Fapdf;
Fapdf -->Gapdf[Final Result];
A -- Excel --> Bex[Extract Excel];
Bex --> Cex[Sheet CSV];
Cex-- <= Max Token --> Dex[CSV Interpreter];
Dex-->Eex[Final Result];
Cex-- >= Max Token -->Fex[Split with token];
Fex-->Dex;
Cex-- Image ? --> Gex[OCR Figure];
Gex-->Eex;
A -- Word --> C[Extract Word];
C-- DOCX ? -->Bwo[ Extract from DOCX];
C-- DOC ? -->Cwo[Extract from DOC];
Bwo-->Dwo[Text];
Bwo-->Iwo[Table];
Bwo-->Gwo[Graph];
Bwo-->Ewo[Figure];
Bwo-->Hwo[Smart Art];
Bwo-->Fwo[Catalog];
Iwo-->Jwo[CSV Interpreter];
Ewo-->Kwo[OCR Figure];
Gwo-->Jwo;
Dwo-->Lwo[Result];
Jwo-->Lwo;
Hwo-->Lwo;
Fwo-->Lwo;
Kwo-->Lwo;
Lwo--No Error ? -->Nwo[Final Result];
Lwo--Error ? -->Mwo[Extract PDF];
Cwo-->Mwo;
Mwo-->Nwo;
A -- PowerPoint --> Bppt[Extract from PPTX];
Bppt-->Cppt[Extract One Slide];
Cppt-->Dppt[Extract different type];
Dppt-->Eppt[Placeholder];
Eppt-->Fppt;
Eppt-->Gppt;
Dppt-->Fppt[Text];
Dppt-->Gppt[Image];
Dppt-->Hppt[Table];
Dppt-->Ippt[Chart];
Dppt-->Jppt[Smart Art];
Gppt-->Kppt[OCR Figure];
Fppt-->Lppt[Recompose Slide];
Kppt-->Lppt;
Hppt-->Lppt;
Ippt-->Lppt;
Jppt-->Lppt;
Lppt-->Mppt[Result for one slide];
Mppt-->Nppt[Final result]






