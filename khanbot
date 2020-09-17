from selenium import webdriver
import pickle
import time

options = webdriver.ChromeOptions()
options.add_argument("user-data-dir=/home/lawrence/.config/google-chrome/Default")
driver = webdriver.Chrome(chrome_options=options)
link = "https://www.khanacademy.org/math/ap-statistics/two-sample-inference?open=1#two-sample-inference-quiz-2"

answer_dict = {}

while True:
    driver.get(link)
    time.sleep(5)
    try:
        driver.find_element_by_xpath("//button[@data-test-id='letsgo-button']").click()
    except:
        pass
    time.sleep(1)
    try:

        while True:
            question = driver.find_element_by_xpath("//div[@data-perseus-paragraph-index='0']").text
            #if question in answer_dict and "all" not in driver.find_element_by_xpath("//div[@class='instructions _125m8j1']"):
            if question in answer_dict:
                print("knows answer")
                #answer is known

                for n in range(10):
                    #"//div[@class='checkbox-and-option _tqugjn']//span[@class='perseus-radio-option-content perseus-interactive']"
                    if driver.find_elements_by_xpath("//span[@class='perseus-radio-option-content perseus-interactive']")[n].text == answer_dict[question]:
                        driver.find_elements_by_xpath("//span[@class='perseus-radio-option-content perseus-interactive']")[n].click()
                        driver.find_element_by_xpath("//button[@data-test-id='exercise-check-answer']").click()
                        driver.find_element_by_xpath("//button[@data-test-id='exercise-next-question']").click()
                        break
            else:
                text = ""
                for n in range(10):
                        # guess a random answer
                        text = driver.find_elements_by_xpath("//span[@class='perseus-radio-option-content perseus-interactive']")[n].text
                        driver.find_elements_by_xpath("//span[@class='perseus-radio-option-content perseus-interactive']")[n].click()
                        driver.find_element_by_xpath("//button[@data-test-id='exercise-check-answer']").click()
                        #continues if guessed it wrong
                        try:
                            driver.find_element_by_xpath("//button[@data-test-id='exercise-check-answer']").click()
                        except Exception as e:
                            # happens if guessed it right
                            answer_dict[driver.find_element_by_xpath("//div[@data-perseus-paragraph-index='0']").text] = text
                            driver.find_element_by_xpath("//button[@data-test-id='exercise-next-question']").click()
                            # continue to next question
                            break
    except Exception as e:
        pass
