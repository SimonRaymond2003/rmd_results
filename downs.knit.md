---
title: "clustering_4th_3rd"
output: html_document
date: "2025-02-26"
---

The goal of this is to have 4th down and third down data... then cluster so see if we can distinguish


Load the outcome data and third down data


``` r
# library(data.table)
# library(randomForest)
# library(pROC)
# 
# # Load the data
# outcome_data <- fread("predict_outcome.csv.gz")
# ctd1 <- fread("predict_ctd1.csv.gz")
# 
# # Select only 1000 rows randomly from each
# outcome_data <- outcome_data[sample(.N, 1000)]  # .N is data.table syntax for the number of rows
# ctd1 <- ctd1[sample(.N, 1000)]  # Corrected the missing parenthesis
# 
# # Add a down column to each dataset before binding
# outcome_data[, down := 1]  # All rows from outcome_data get down = 1
# ctd1[, down := 0]          # All rows from ctd1 get down = 0
# 
# # Find common columns between the two datasets (now including down)
# common_cols <- intersect(names(outcome_data), names(ctd1))
# 
# # Create a new data table with only the common columns from both datasets
# data <- rbind(
#   outcome_data[, ..common_cols],
#   ctd1[, ..common_cols]
# )
# 
# # From data grab only offense/defense_player_x/xx_ cols and down
# player_cols <- grep("offense_player_|defense_player_", names(data), value = TRUE)
# data <- data[, .SD, .SDcols = c("down", player_cols)]  # .SDcols selects specific columns
# 
# # Convert 'down' to a factor for classification
# data[, down := as.factor(down)]
# 
# # Subset the data for normal players and starters
# normal_player_cols <- grep("offense_player_|defense_player_", names(data), value = TRUE)
# starter_player_cols <- grep("starter_offense_player_|starter_defense_player_", names(data), value = TRUE)
# 
# normal_data <- data[, .SD, .SDcols = c("down", normal_player_cols)]
# starter_data <- data[, .SD, .SDcols = c("down", starter_player_cols)]
# 
# # Function to run Random Forest, calculate OOB AUC, and return importance matrix
# run_rf <- function(data) {
#   rf_model <- randomForest(down ~ ., data = data, ntree = 1, importance = TRUE, keep.forest = TRUE, oob.prox = TRUE)
#   oob_predictions <- rf_model$votes[, 2] # Probabilities for the second class
#   oob_auc <- auc(data$down, oob_predictions)
#   importance_matrix <- importance(rf_model)  # Extract importance matrix
#   return(list(oob_auc = oob_auc, importance_matrix = importance_matrix))
# }
# 
# # Run Random Forest on normal players data
# normal_results <- run_rf(normal_data)
# normal_auc <- normal_results$oob_auc
# normal_importance_matrix <- normal_results$importance_matrix
# print(paste("OOB AUC for normal players:", normal_auc))
# 
# # Run Random Forest on starters data
# starter_results <- run_rf(starter_data)
# starter_auc <- starter_results$oob_auc
# starter_importance_matrix <- starter_results$importance_matrix
# print(paste("OOB AUC for starters:", starter_auc))
# 
# # Print importance matrices
# print("Importance matrix for normal players:")
# print(normal_importance_matrix)
# 
# print("Importance matrix for starters:")
# print(starter_importance_matrix)
```


