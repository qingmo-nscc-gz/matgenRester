# matgen_rester
A python wrapper for Matgen DFT API. This code requires a python version >= 3.6

## Prerequisites

The following python library must be installed to run the script

* [requests](https://requests.readthedocs.io/en/master/)
* [PyYaml](https://pypi.org/project/PyYAML/)
* [numpy](https://pypi.org/project/numpy/)

## installation
`pip install matgen-rester`

## Usage
### 1. import matgen_rester module
`import matgen_rester as mr`

#### example
```
with mr.MatgenRester(username="test",password="only for example") as q:
   ##return list with one structure
   structure = q.get_structure_by_matid(matid='mat_3',fields=["matid","formula"])
   ##return list of data
   list = q.get_structure_with_filter(elements="Ba-S", filter={
    "in": "Na-O",
    "not": "C",
    "searchType": "all",
    "crystalSystem": [
      "cubic",
      "hexagonal",
      "monoclinic",
      "orthorhombic",
      "tetragonal",
      "triclinic",
      "trigonal"
    ],
    "pointGroup": [
      "-1",
      "-3",
      "-3m",
      "-4",
      "-42m",
      "-43m",
      "-6",
      "-6m2",
      "1",
      "2",
      "2/m",
      "222",
      "23",
      "3",
      "32",
      "3m",
      "4",
      "4/m",
      "4/mmm",
      "422",
      "432",
      "4mm",
      "6",
      "6/m",
      "6/mmm",
      "622",
      "6mm",
      "m",
      "m-3",
      "m-3m",
      "mm2",
      "mmm"
    ],
    "spaceGroup": [
      "Aea2",
      "Aem2",
      "R3m"
    ],
    "volume": [
      0,
      10000
    ],
    "properties": [
      "cif",
      "xrd.x"
    ],
    "ifIcsdid": True
   }, fields=['matid'], size=5, page=0)
```

#### attributes
1. `username, password`: matgen account
2. `token`: user can get token key after logged in from [matgen](https://matgen.nscc-gz.cn)
3. `id`: the target id of the structure
4. `idType`: type of the target id, such as matid
5. `fields`: return data fields, such as "structure","bandStructure","densityOfStates","cif", "elasticProperty","fermiSurface","magneticProperty","pdf","xrd"
6. `filter`: filter dic for searching structure, such as "in", "not","searchType"
7. `size`: the size of return records
8. `pindex`: the page index after pagination

### 2. used in command line

#### example
`python matgenrester.py -id mat_3 -idType matid`

#### optional arguments:
```
  -h, --help            show this help message and exit
  -idType IDTYPE, --idType IDTYPE
                        specify the idType for search, such as matid, icsd_id,
                        cod_id, oqmd_id
  -id ID, --id ID       find the structure with the target id,such as mat_8886
                        as matid
  -size SIZE, --size SIZE
                        specify the number of return data
  -pindex PINDEX, --pindex PINDEX
                        specify the page index after pagination
  -in IN, --in IN       find the structures that contain the specific
                        elements, for more than one elements, connect elements
                        by '-', ex. Ba-S
  -not NOT, --not NOT   find the structures that don't contain the specific
                        elements, for more than one elements, connect elements
                        by '-', ex. Ba-S
  -searchType SEARCHTYPE, --searchType SEARCHTYPE
                        specify the search type for searching structures,
                        'only' means finding the structures that only contain
                        the specific elements, 'all' means finding the
                        structures that not only contain the specific
                        elements, but also, sometimes, other elements
  -crystalSystem CRYSTALSYSTEM, --crystalSystem CRYSTALSYSTEM
                        filter data by its crystal_system, such as cubic,tetra
                        gonal,hexagonal,trigonal,orthorhombic,monoclinic,tricl
                        inic,amorphous
  -pointGroup POINTGROUP, --pointGroup POINTGROUP
                        filter data by its point_group, such as cubic,tetragon
                        al,hexagonal,trigonal,orthorhombic,monoclinic,triclini
                        c,amorphous
  -spacegroup SPACEGROUP, --spacegroup SPACEGROUP
                        filter data by its spacegroup, specify space group
                        type, such as P1,P-1,P2,P21,C2,Pm,Pc,Cm,Cc,P2/m,P21m,P
                        2/c,P21c,C2/m,C2/c,P222,P2221,P21212,P212121,C222,C222
                        1,F222,I222,I212121,Pmm2,Pmc21,Pcc2,Pma2,Pca21,Pnc2,Pm
                        n21,Pba2,Pna21,Pnn2,Cmm2,Cmc21,Ccc2,Amm2,Abm2,Ama2,Aba
                        2,Fmm2,Fdd2,Imm2,Iba2,Ima2,Pmmm,Pnnn,Pccm,Pban,Pmma,Pn
                        na,Pmna,Pcca,Pbam,Pccn,Pbcm,Pnnm,Pmmn,Pbcn,Pbca,Pnma,C
                        mmm,Cmcm,Cmca,Cccm,Cmma,Ccca,Fmmm,Fddd,Immm,Ibam,Ibcm,
                        Imma,P4,P41,P42,P43,I4,I41,P-4,I-4,P4/m,P42/m,P4/n,P42
                        /n,I4/m,I41/a,P422,P4212,P4122,P41212,P4222,P42212,P43
                        22,P43212,I422,I4212,P4mm,P4bm,P42cm,P42nm,P4cc,P4nc,P
                        42mc,P42bc,I4mm,I4cm,I41md,I41cd,P-42m,P-42c,P-421m,P-
                        421c,I-42m,I-42d,P-4m2,P-4c2,P-4b2,P-4n2,I-4m2,I-4c2,P
                        4/mmm,P4/mcc,P4/nbm,P4/nnc,P4/mbm,P4/mnc,P4/nmm,P4/ncc
                        ,P42/mmc,P42/mcm,P42/nbc,P42/nnm,P42/mbc,P42/mcm,P42/n
                        mc,P42/ncm,I4/mmm,I4/mcm,I41/amd,I41/acd,P3,P31,P32,R3
                        ,P-3,R-3,P312,P3112,P3212,P321,P3121,P3221,R32,P31m,P3
                        1c,P3m1,P3c1,R3m,R3c,P-31m,P-31c,P-3m1,P-3c1,R-3m,R-3c
                        ,P6,P61,P62,P63,P64,P65,P-6,P6/m,P63/m,P622,P6122,P622
                        2,P6322,P6422,P6522,P6mm,P6cc,P63cm,P63mc,P-6m2,P-6c2,
                        P-62m,P62c,P6/mmm,P6/mcc,P63/mcm,P63/mmc,P23,P213,F23,
                        I23,I213,Pm-3,Pn-3,Pa-3,Fm-3,Fd-3,Im-3,Ia-3,P432,P4232
                        ,P4332,P4132,F432,F4132,I432,I4132,P-43m,P-43n,F-43m,F
                        -43c,I-43m,I-43d,Pm-3m,Pn-3n,Pm-3n,Pn-3m,Fm-3m,Fm-3m,F
                        d-3m,Fd-3c,Im-3m,Ia-3d
  -volume VOLUME, --volume VOLUME
                        filter data by its volume, specify volume scope, such
                        as '0,100'
  -density DENSITY, --density DENSITY
                        filter data by its density, specify volume scope, such
                        as '0,100'
  -icsdid ICSDID, --icsdid ICSDID
                        filter data if it contains a icsdid
  -codid CODID, --codid CODID
                        filter data if it contains a codid
  -oqmdid OQMDID, --oqmdid OQMDID
                        filter data if it contains a oqmdid
  -fields FIELDS, --fields FIELDS
                        specify return data fields, such as 'structure',
                        'bandStructure', 'densityOfStates', 'cif',
                        'elasticProperty', 'fermiSurface', 'magneticProperty',
                        'pdf', 'xrd'
  -o O                  set file for downloading
  -token TOKEN, --token TOKEN
                        upload matgen token for seaching```