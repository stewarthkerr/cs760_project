TIMEPOINTS ?= 2
REPS ?= 2
THRESHOLD ?= 0.02
EXPRESSION ?= average

gold_at:
		./generate_gold.py -i ../data/Arab.Meristem/arabidopsis.meristem.expression.csv -c "Feature_ID" --delimiter=',' -o ../data/Arab.Meristem/arabidopsis.meristem.biogrid.interactions.csv --pickle ../data/Arab.Meristem/arabidopsis.meristem.biogrid.graph.pickle

gold_atd:
		python3 -m pdb ./generate_gold.py -i ../data/Arab.Meristem/arabidopsis.meristem.expression.csv -c "Feature_ID" --delimiter=',' -o ../data/Arab.Meristem/arabidopsis.meristem.biogrid.interactions.csv --pickle ../data/Arab.Meristem/arabidopsis.meristem.biogrid.graph.pickle

gold_atrm:
		./generate_gold_atrm.py -i ../data/ATRM/Regulations_in_ATRM.csv --delimiter=',' -o ../data/ATRM/Regulations_in_ATRM.adjacency.csv --pickle ../data/ATRM/Regulations_in_ATRM.adjacency.pickle

gold_atrmd:
		python3 -m pdb ./generate_gold_atrm.py -i ../data/ATRM/Regulations_in_ATRM.csv --delimiter=',' -o ../data/ATRM/Regulations_in_ATRM.adjacency.csv --pickle ../data/ATRM/Regulations_in_ATRM.adjacency.pickle

gold_cpib:
		./generate_gold.py -i ../data/CPIB_Lateral_Root_timecourse/E-MTAB-2565-A-AFFY-2-normalized-expressions.tsv -o ../data/CPIB_Lateral_Root_timecourse/CPIB_Lateral_Root.biogrid.interactions.csv --pickle ../data/CPIB_Lateral_Root_timecourse/CPIB_Lateral_Root_timecourse.biogrid.graph.pickle

gold_cpibd:
		python3 -m pdb ./generate_gold.py -i ../data/CPIB_Lateral_Root_timecourse/E-MTAB-2565-A-AFFY-2-normalized-expressions.tsv -o ../data/CPIB_Lateral_Root_timecourse/CPIB_Lateral_Root.biogrid.interactions.csv --pickle ../data/CPIB_Lateral_Root_timecourse/CPIB_Lateral_Root_timecourse.biogrid.graph.pickle

cluster2csv:
	 R CMD BATCH cluster2csv.R

golden4cluster_at:
		./golden2cluster.py -i ../data/Arab.Meristem/arabidopsis.meristem.expression.csv -c "Feature_ID" --delimiter=',' --cluster ../output/Clustering.csv -o ../data/Arab.Meristem/arabidopsis.meristem.modules.interactions.csv --pickle ../data/Arab.Meristem/arabidopsis.meristem.biogrid.graph.pickle --opickle ../data/Arab.Meristem/arabidopsis.meristem.modules.graph.pickle

golden2cluster_atd:
		python3 -m pdb ./golden2cluster.py -i ../data/Arab.Meristem/arabidopsis.meristem.expression.csv -c "Feature_ID" --delimiter=',' --cluster ../output/Clustering.csv -o ../data/ --pickle ../data/Arab.Meristem/arabidopsis.meristem.biogrid.graph.pickle --opickle ../data/

golden2cluster_atrm:
		./golden2cluster.py -i ../data/Arab.Meristem/arabidopsis.meristem.expression.csv -c "Feature_ID" --delimiter=',' --cluster ../output/Clustering.csv -o ../data/ATRM/Regulations_in_ATRM.adjacency.modules.csv --pickle ../data/ATRM/Regulations_in_ATRM.adjacency.pickle --opickle ../data/ATRM/Regulations_in_ATRM.adjacency.modules.pickle

golden2cluster_atrmd:
		python3 -m pdb ./golden2cluster.py -i ../data/Arab.Meristem/arabidopsis.meristem.expression.csv -c "Feature_ID" --delimiter=',' --cluster ../output/Clustering.csv -o ../data/ATRM/Regulations_in_ATRM.adjacency.modules.csv --pickle ../data/ATRM/Regulations_in_ATRM.adjacency.pickle --opickle ../data/ATRM/Regulations_in_ATRM.adjacency.modules.pickle

goldenThreshold_at:
		./goldenThreshold.py -o ../data/Arab.Meristem/arabidopsis.meristem.modules.interactions.t$(THRESHOLD).tsv --pickle ../data/Arab.Meristem/arabidopsis.meristem.modules.graph.pickle --threshold $(THRESHOLD)

goldenThreshold_atd:
		python3 -m pdb ./goldenThreshold.py -o ../data/Arab.Meristem/arabidopsis.meristem.modules.interactions.t$(THRESHOLD).tsv --pickle ../data/Arab.Meristem/arabidopsis.meristem.modules.graph.pickle --threshold $(THRESHOLD)

goldenThreshold_atrm:
		./goldenThreshold.py -o ../data/ATRM/Regulations_in_ATRM.modules.interactions.t$(THRESHOLD).tsv --pickle ../data/ATRM/Regulations_in_ATRM.adjacency.modules.pickle --threshold $(THRESHOLD)

goldenThreshold_atrmd:
		python3 -m pdb ./goldenThreshold.py -o ../data/ATRM/Regulations_in_ATRM.modules.interactions.t$(THRESHOLD).tsv --pickle ../data/ATRM/Regulations_in_ATRM.adjacency.modules.pickle --threshold $(THRESHOLD)

analysis_at:
	 R CMD BATCH '--args expression="$(EXPRESSION)" n_dbn_timepoints=$(TIMEPOINTS) n_reps=$(REPS) g_file="../data/Arab.Meristem/arabidopsis.meristem.modules.interactions.t$(THRESHOLD).tsv" d_path="../output/Clustering.RDATA.RData"' arab.meristem.analysis.R

analysis_atrm:
	 R CMD BATCH '--args expression="$(EXPRESSION)" n_dbn_timepoints=$(TIMEPOINTS) n_reps=$(REPS) g_file="../data/ATRM/Regulations_in_ATRM.modules.interactions.t$(THRESHOLD).tsv" d_path="../output/Clustering.RDATA.RData"' arab.meristem.analysis.R

cluster2expression_at:
	 R CMD BATCH '--args num_reps=20' cluster2expression.R

perf_at:
		R CMD BATCH '--args g_file=\"../data/Arab.Meristem/arabidopsis.meristem.modules.interactions.t$(THRESHOLD).tsv\" save_file="../output/arab.meristem.analysis.$(EXPRESSION).$(TIMEPOINTS).RData"' arab.meristem.perf.R

clean:
	rm *.Rout
