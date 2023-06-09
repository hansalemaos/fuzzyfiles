# Binary fuzzy matching in all file types [fzf (pre-filter)/rapidfuzz (finds the best result)]

### Tested against Windows 10 / Python 3.10 / Anaconda


#### pip install fuzzyfiles



Download FZF: https://github.com/junegunn/fzf 

PIP Install: https://github.com/maxbachmann/RapidFuzz
(Visual C++ 2019 redistributable is required)


```python

# IMPORTANT: 	The script must be inside a py file, it does not work directly from the console!

from list_all_files_recursively import get_folder_file_complete_path
from fuzzyfiles import fuzzy_file_search

fzf_path = r"C:\fzf.exe"
querylist = [
    "Es war einmal",
    "Was machst du?",
    "Wir müssen hierbleiben!",
    "Er kaufte ein Haus",
]

files = [x.path for x in get_folder_file_complete_path(r"E:\meinebuecher")]
df = fuzzy_file_search(
    querylist,
    files,
    fzf_path,
    fzfargs=("-i",),
    shell=False,
    close_fds=False,
    start_new_session=True,
    bufsize=8192 * 10,
    invisible=True,
    timeout=60,
    max_threads=None,
    timeout_check_sleep=3,
    kill_all_at_end=True,
    blockbatch=False,
)

print(files)

print(df.to_string(max_colwidth=40))


# ['E:\\meinebuecher\\Adorf_Mario_Der_Dieb_von_Trastevere_Geschichten_aus_Italien1.txt', 'E:\\meinebuecher\\Adorf_Mario_Der_Dieb_von_Trastevere_Geschichten_aus_Italien10000000.pkl', 'E:\\meinebuecher\\Adorf_Mario_Der_Mäusetöter_Unrühmliche_Geschichten1.txt', 'E:\\meinebuecher\\Adorf_Mario_Himmel_und_Erde_Unordentliche_Erinnerungen.txt', 'E:\\meinebuecher\\Ad_Daula_al_Islāmīya_Todenhöfer_Jürgen_Inside_IS_10_Tage_im_Islamischen_Staat_.txt', 'E:\\meinebuecher\\Allan_Pease_Barbara_Pease_Warum_Manner_nicht_zuhoren_und_Frauen_schlecht_einparken.pdf', 'E:\\meinebuecher\\Andreas_Eschbach_Eine_Trillion_Euro.pdf', 'E:\\meinebuecher\\Andreas_Meier_Henrik_Stormer_eBusiness_eCommerce_Management_der_digitalen_Wertschöpfungskette_1Auflage.pdf', 'E:\\meinebuecher\\Arthur_Hailey_Hotel.pdf']
#                        searchbinsplit      score                          searchbin                             match_detail                                 filepath                                    match  src_start  src_end  dest_start  dest_end             searchstring stderr  returncode
# 0                   b'Was machst du?'  71.428571                  b'Was machst du?'                     b'\\xbbWas hast du d'  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'Sam packte seinen Koffer, ging dan...       4222     4236           0        14           Was machst du?    b''           0
# 1   b'Wir m\\xc3\\xbcssen hierbleiben!'  70.833333  b'Wir m\\xc3\\xbcssen hierbleiben!'        b'r. Wir m\\xc3\\xbcssen leider no'  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'Enrico war in Florenz geblieben, u...      17192    17216           0        24  Wir müssen hierbleiben!    b''           0
# 2                    b'Es war einmal'  76.923077                   b'Es war einmal'                      b'\\x00Es war eine '  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'\\xc2\\xbbWieso k\\xc3\\xb6nnen Sie be...     131842   131855           0        13            Es war einmal    b''           0
# 3               b'Er kaufte ein Haus'  72.222222              b'Er kaufte ein Haus'                    b'hler hat kein Haus'  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'Eines Nachts h\\xc3\\xb6rte ich ein ...       5351     5369           0        18       Er kaufte ein Haus    b''           0
# 4                   b'Was machst du?'  42.857143                  b'Was machst du?'                        b"anders', 'Nach"  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'Filmfestsp\\xc3\\xb6\\xc3\\xaeIele\\xc3...      23968    23982           0        14           Was machst du?    b''           0
# 5   b'Wir m\\xc3\\xbcssen hierbleiben!'  54.166667  b'Wir m\\xc3\\xbcssen hierbleiben!'           b'gisseur von Diebe haben\\xc3'  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'Ndherberge\\xc3\\xb6\\xc3\\xa7\\xc3\\xb6...       7513     7537           0        24  Wir müssen hierbleiben!    b''           0
# 6                    b'Es war einmal'  76.923077                   b'Es war einmal'                         b's waren damal'  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'/./&/ \\xc3\\xb6hjM\\xc2\\xa4\\xc5\\xaf\...       2883     2896           0        13            Es war einmal    b''           0
# 7               b'Er kaufte ein Haus'  61.111111              b'Er kaufte ein Haus'                    b'raf ich auf ein ga'  E:\meinebuecher\Adorf_Mario_Der_Dieb...  b'/./&/ \\xc3\\xb6hjM\\xc2\\xa4\\xc5\\xaf\...       5835     5853           0        18       Er kaufte ein Haus    b''           0
# 8                   b'Was machst du?'  71.428571                  b'Was machst du?'                        b'l brauchst du?'  E:\meinebuecher\Adorf_Mario_Der_Mäus...  b'In jenen Tagen war meine Miete \\xc...       1398     1412           0        14           Was machst du?    b''           0
# 9   b'Wir m\\xc3\\xbcssen hierbleiben!'  62.500000  b'Wir m\\xc3\\xbcssen hierbleiben!'  b'inute hierbleiben \\xe2\\x80\\xa6!\\xc...  E:\meinebuecher\Adorf_Mario_Der_Mäus...  b'Bis weit in den achten Monat hinei...       1476     1500           0        24  Wir müssen hierbleiben!    b''           0
# 10                   b'Es war einmal'  76.923077                   b'Es war einmal'                         b' wir einmal e'  E:\meinebuecher\Adorf_Mario_Der_Mäus...  b'Und es folgte unweigerlich eine br...      60416    60429           0        13            Es war einmal    b''           0
# 11              b'Er kaufte ein Haus'  72.222222              b'Er kaufte ein Haus'                    b' Er hatte in Hambu'  E:\meinebuecher\Adorf_Mario_Der_Mäus...  b'Zwei Monate sp\\xc3\\xa4ter war er t...      87656    87674           0        18       Er kaufte ein Haus    b''           0
# 12                  b'Was machst du?'  92.857143                  b'Was machst du?'                     b'\\xbbWas machst du'  E:\meinebuecher\Adorf_Mario_Himmel_u...  b"Mein Freund Peter Berling rief mic...         41       55           0        14           Was machst du?    b''           0
# 13  b'Wir m\\xc3\\xbcssen hierbleiben!'  62.500000  b'Wir m\\xc3\\xbcssen hierbleiben!'        b'e m\\xc3\\xbcssen mir nun zeigen'  E:\meinebuecher\Adorf_Mario_Himmel_u...  b"Der franz\\xc3\\xb6sische Regisseur ...      42156    42180           0        24  Wir müssen hierbleiben!    b''           0
# 14                   b'Es war einmal'  92.307692                   b'Es war einmal'                         b'Es war ein al'  E:\meinebuecher\Adorf_Mario_Himmel_u...  b"Ich wachte auf, als das Telefon l\...     120432   120445           0        13            Es war einmal    b''           0
# 15              b'Er kaufte ein Haus'  72.222222              b'Er kaufte ein Haus'                    b'ur auf meine Hands'  E:\meinebuecher\Adorf_Mario_Himmel_u...  b"Wodka konnte man auch ganz legal i...     260770   260788           0        18       Er kaufte ein Haus    b''           0
# 16                  b'Was machst du?'  78.571429                  b'Was machst du?'               b'\\xc2\\xab\\x00Was macht d'  E:\meinebuecher\Ad_Daula_al_Islāmīya...  b'11 \\xc2\\xbbIch werde dir jetzt was...      16651    16665           0        14           Was machst du?    b''           0
# 17  b'Wir m\\xc3\\xbcssen hierbleiben!'  66.666667  b'Wir m\\xc3\\xbcssen hierbleiben!'     b' Wir m\\xc3\\xbcssen lachen.\\x00Bei'  E:\meinebuecher\Ad_Daula_al_Islāmīya...  b'Sollte ich auf einen solch pharis\...       6124     6148           0        24  Wir müssen hierbleiben!    b''           0
# 18                   b'Es war einmal'  76.923077                   b'Es war einmal'                         b'en wir einmal'  E:\meinebuecher\Ad_Daula_al_Islāmīya...  b'Unser tief vermummter Fahrer spric...      15114    15127           0        13            Es war einmal    b''           0
# 19              b'Er kaufte ein Haus'  72.222222              b'Er kaufte ein Haus'                    b'rkt, kaufen ein pa'  E:\meinebuecher\Ad_Daula_al_Islāmīya...  b'Am n\\xc3\\xa4chsten Tag beim Mittag...     142527   142545           0        18       Er kaufte ein Haus    b''           0
# 20                  b'Was machst du?'  42.857143                  b'Was machst du?'                       b'ages \r/Parent '  E:\meinebuecher\Allan_Pease_Barbara_...  b'4I/\\x16j \\xef\\xbf\\xbd\\x0be\\xef\\xbf...     231293   231307           0        14           Was machst du?    b''           0
# 21  b'Wir m\\xc3\\xbcssen hierbleiben!'  12.500000  b'Wir m\\xc3\\xbcssen hierbleiben!'  b'\\xc3\\xbcR\\x18\\\\xef\\xbf\\xbd.\\xef\\x...  E:\meinebuecher\Allan_Pease_Barbara_...  b'.\\xef\\xbf\\xbd\\xef\\xbf\\xbdW\\xef\\xbf...       1011     1035           0        24  Wir müssen hierbleiben!    b''           0
# 22                   b'Es war einmal'  46.153846                   b'Es war einmal'                        b'es \r/Parent 1'  E:\meinebuecher\Allan_Pease_Barbara_...  b'7\\x11\\xef\\xbf\\xbd\\xca\\xb4-\\xef\\xbf...        643      656           0        13            Es war einmal    b''           0
# 23              b'Er kaufte ein Haus'  38.888889              b'Er kaufte ein Haus'                    b'r /FlateDecode >> '  E:\meinebuecher\Allan_Pease_Barbara_...  b'1\\xef\\xbf\\xbd\\xd6\\x95\\xde\\x9dJce\\x...     342383   342401           0        18       Er kaufte ein Haus    b''           0
# 24                  b'Was machst du?'  50.000000                  b'Was machst du?'                        b'(Wer bezahlt d'  E:\meinebuecher\Andreas_Eschbach_Ein...  b'1398 0 obj<</CreationDate(D:200607...       2544     2558           0        14           Was machst du?    b''           0
# 25  b'Wir m\\xc3\\xbcssen hierbleiben!'   0.000000  b'Wir m\\xc3\\xbcssen hierbleiben!'                                      b''  E:\meinebuecher\Andreas_Eschbach_Ein...                                      b''          0        0           0         0  Wir müssen hierbleiben!    b''           1
# 26                   b'Es war einmal'  46.153846                   b'Es war einmal'                         b'e(Elia Barcel'  E:\meinebuecher\Andreas_Eschbach_Ein...  b'1398 0 obj<</CreationDate(D:200607...       1153     1166           0        13            Es war einmal    b''           0
# 27              b'Er kaufte ein Haus'  50.000000              b'Er kaufte ein Haus'           b' Mauer f\\xef\\xbf\\xbdr eine '  E:\meinebuecher\Andreas_Eschbach_Ein...  b'1398 0 obj<</CreationDate(D:200607...       5106     5124           0        18       Er kaufte ein Haus    b''           0
# 28                  b'Was machst du?'  35.714286                  b'Was machst du?'                       b'age \r/Rotate 0'  E:\meinebuecher\Andreas_Meier_Henrik...  b'DuG=(V/34Ri4ElnKaQD?.XXWB8A-_olH=3...     104521   104535           0        14           Was machst du?    b''           0
# 29  b'Wir m\\xc3\\xbcssen hierbleiben!'   0.000000  b'Wir m\\xc3\\xbcssen hierbleiben!'                                      b''  E:\meinebuecher\Andreas_Meier_Henrik...                                      b''          0        0           0         0  Wir müssen hierbleiben!    b''           1
# 30                   b'Es war einmal'  53.846154                   b'Es war einmal'                         b' Professional'  E:\meinebuecher\Andreas_Meier_Henrik...  b'endstream\rendobj\r2870 0 obj\r<< ...     588980   588993           0        13            Es war einmal    b''           0
# 31              b'Er kaufte ein Haus'  50.000000              b'Er kaufte ein Haus'                   b'reater \r/question '  E:\meinebuecher\Andreas_Meier_Henrik...  b'\\xef\\xbf\\xbdh5vT\\xef\\xbf\\xbd %]\\xe...      20093    20111           0        18       Er kaufte ein Haus    b''           0
# 32                  b'Was machst du?'  28.571429                  b'Was machst du?'  b'\\xbf\\xbd7sa\\xef\\xbf\\xbds\\xef\\xbf\\x...  E:\meinebuecher\Arthur_Hailey_Hotel.pdf  b'\\xef\\xbf\\xbdy_V~\\xef\\xbf\\xbdt\\xef\...     190781   190795           0        14           Was machst du?    b''           0
# 33  b'Wir m\\xc3\\xbcssen hierbleiben!'   0.000000  b'Wir m\\xc3\\xbcssen hierbleiben!'                                      b''  E:\meinebuecher\Arthur_Hailey_Hotel.pdf                                      b''          0        0           0         0  Wir müssen hierbleiben!    b''           1
# 34                   b'Es war einmal'  46.153846                   b'Es war einmal'                         b'Es ist Montag'  E:\meinebuecher\Arthur_Hailey_Hotel.pdf  b'\\xef\\xbf\\xbd\\xef\\xbf\\xbd\\xef\\xbf\\x...      13612    13625           0        13            Es war einmal    b''           0
# 35              b'Er kaufte ein Haus'  27.777778              b'Er kaufte ein Haus'  b'\\xbf\\xbdr\\x10\\xef\\xbf\\xbd\\xef\\xbf\...  E:\meinebuecher\Arthur_Hailey_Hotel.pdf  b'\\xef\\xbf\\xbd\\xef\\xbf\\xbdg\\xef\\xbf\...     109500   109518           0        18       Er kaufte ein Haus    b''           0

    Args:
        querylist (list): List of queries to search for.

            Token	     Match type					        Description
            sbtrkt	     fuzzy-match				        Items that match sbtrkt
            'wild	     exact-match (quoted)		        Items that include wild
            ^music	     prefix-exact-match			        Items that start with music
            .mp3$	     suffix-exact-match			        Items that end with .mp3
            !fire	     inverse-exact-match		        Items that do not include fire
            !^music	     inverse-prefix-exact-match	        Items that do not start with music
            !.mp3$	     inverse-suffix-exact-match	        Items that do not end with .mp3

            A single bar character term acts as an OR operator. For example, the following query matches entries that
             start with core and end with either go, rb, or py.

            ^core go$ | rb$ | py$
            VERY IMPORTANT: ---- SPACE BEFORE and AFTER the single bar character term

            More information here: https://github.com/junegunn/fzf


        files (str | list | tuple): Path(s) to file(s) to search in.
        fzf_path (str, optional): Path to the fzf executable. Defaults to "fzf.exe".
        fzfargs (tuple, optional): Additional arguments to pass to fzf. Defaults to ("-i",).
        shell (bool, optional): Whether to use a shell to execute the command. Defaults to False.
        close_fds (bool, optional): Whether to close file descriptors. Defaults to False.
        start_new_session (bool, optional): Whether to start a new session. Defaults to True.
        bufsize (int, optional): Buffer size. Defaults to 8192 * 4.
        invisible (bool, optional): Whether to run the command invisibly (no window). Defaults to True.
        timeout (int, optional): Timeout in seconds. Defaults to 60.
        max_threads (int | None, optional): Maximum number of threads to use. Defaults to None (number of CPUs).
        timeout_check_sleep (int | float, optional): Time to sleep between timeout checks. Defaults to 3.
        kill_all_at_end (bool, optional): Whether to kill all not finished processes at the end. Defaults to True.
        blockbatch (bool, optional): Whether to block batch processing. Defaults to False.

    Returns:
        pd.DataFrame: A dataframe containing the search results.

```