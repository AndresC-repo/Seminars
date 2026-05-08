.PHONY: help run down logs clean restart

# Colors for pretty output
BLUE := \033[0;34m
GREEN := \033[0;32m
YELLOW := \033[0;33m
RED := \033[0;31m
NC := \033[0m # No Color


help:
	@echo "$(BLUE)Permutation Feature Importance$(NC)"
	@echo ""
	@echo "$(GREEN)Docker Related Commands:$(NC)"
	@echo "  make build"
	@echo "      $(YELLOW)Builds the application using Docker Compose.$(NC)"
	@echo "  make up"
	@echo "      $(YELLOW)Runs the application using Docker Compose.$(NC)"
	@echo "  make down"
	@echo "      $(YELLOW)Stops the running application.$(NC)"
	@echo "  make logs"
	@echo "      $(YELLOW)Tails the logs of the running application.$(NC)"
	@echo "  make clean"
	@echo "      $(YELLOW)Cleans up all Docker resources (containers, images, volumes).$(NC)"
	@echo "  make restart"
	@echo "      $(YELLOW)Restarts the application by stopping and then starting it again.$(NC)"
	@echo ""


# =============================================================================
# Run
# =============================================================================
build:
	@echo "$(GREEN)Building the application...$(NC)"
	@echo "Open http://localhost:8889 in your browser."
	docker compose up --build

up:
	@echo "$(GREEN)Running the application...$(NC)"
	@echo "Open http://localhost:8889 in your browser."
	docker compose up

down:
	@echo "$(GREEN)Stopping the application...$(NC)"
	docker compose down

logs:
	@echo "$(GREEN)Viewing application logs...$(NC)"
	docker compose logs -f

clean:
	@echo "$(GREEN)Cleaning up Docker resources...$(NC)"
	docker compose down --rmi all --volumes --remove-orphans

restart:
	@echo "$(GREEN)Restarting the application...$(NC)"
	docker compose down && docker compose up --build
