Далее представлена иерархия классов для различных спортивных игр с различными полями, виртуальными функциями, а также, методами.
Имеется наследование, демонстрация работы с объектами различных классов, а также, перегрузка методов.
Также, данный код открыд для реадакции в целях совершенствования.

#include <iostream>
#include <string>

class SportsGame {
protected:
    int players;
    int score;

public:
    SportsGame() : players(0), score(0) {}
    SportsGame(int players, int score) : players(players), score(score) {}
    SportsGame(const SportsGame& game) : players(game.players), score(game.score) {}
    virtual ~SportsGame() {}

    virtual void play() = 0;
    virtual void endGame() {
        std::cout << "Game ended. Final score: " << score << std::endl;
    }

    int getPlayers() const {
        return players;
    }

    int getScore() const {
        return score;
    }

    void setScore(int newScore) {
        score = newScore;
    }

private:
    void privateMethod() {
        std::cout << "Private method called." << std::endl;
    }

public:
    void callPrivateMethod() {
        privateMethod();
    }
};

class Football : public SportsGame {
private:
    static int yellowCards;

public:
    Football() : yellowCards(0) {}
    Football(int players, int score, int yellowCards) : SportsGame(players, score), yellowCards(yellowCards) {}

    void play() override {
        std::cout << "Playing football. Score: " << score << std::endl;
    }

    void giveYellowCard() {
        yellowCards++;
    }

    int getYellowCards() const {
        return yellowCards;
    }
};

int Football::yellowCards = 0;

class Hockey : protected SportsGame {
private:
    std::string location;
    int penaltyMinutes;

public:
    Hockey() : location("Unknown"), penaltyMinutes(0) {}
    Hockey(int players, int score, std::string location, int penaltyMinutes) : SportsGame(players, score), location(location), penaltyMinutes(penaltyMinutes) {}

    void play() override {
        std::cout << "Playing hockey. Score: " << score << std::endl;
    }

    void setPenaltyMinutes(int minutes) {
        penaltyMinutes = minutes;
    }

    int getPenaltyMinutes() const {
        return penaltyMinutes;
    }
};

class BallHockey : public Hockey {
private:
    bool hasStick;

public:
    BallHockey() : hasStick(true) {}
    BallHockey(int players, int score, std::string location, int penaltyMinutes, bool hasStick) : Hockey(players, score, location, penaltyMinutes), hasStick(hasStick) {}

    void play() override {
        std::cout << "Playing ball hockey. Score: " << score << std::endl;
    }

    void useStick() {
        hasStick = true;
    }
};

int main() {
    Football footballGame(22, 0, 1);
    Hockey hockeyGame(12, 0, "Arena", 0);
    BallHockey ballHockeyGame(10, 0, "Outdoor rink", 0, false);

    SportsGame *games[] = {&footballGame, &hockeyGame, &ballHockeyGame};

    int choice;
    do {
        std::cout << "Choose a game to play:" << std::endl;
        std::cout << "1. Football" << std::endl;
        std::cout << "2. Hockey" << std::endl;
        std::cout << "3. Ball Hockey" << std::endl;
        std::cout << "4. Exit" << std::endl;

        std::cin >> choice;

        if (choice >= 1 && choice <= 3) {
            games[choice - 1]->play();
            games[choice - 1]->endGame();
        }
    } while (choice != 4);

    return 0;
