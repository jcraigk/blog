---
title: Finding a Rails Job in 2025
excerpt: A modern tale of software engineer seeks and, after many trials, finds job
header:
  image: /assets/images/posts/2025-04-06-header.jpg
  teaser: /assets/images/posts/2025-04-06-header.jpg
---

This entry summarizes my process of applying to Senior and Staff level software engineering roles during the first 90 days of 2025. It had been almost a decade since my last job search and I found the process surprising in some ways. I'll expound on that later but first: what was I looking for?

I'm a seasoned (read: old) Ruby on Rails engineer, and I still love building stuff in that framework even after 18 years of professional focus, so the stack focus was important in my search. I was seeking a fully remote position or a hybrid role with an office in southern California. I was open to working at a small or mid-sized company, startup or established, and in almost any field as long as the organization wasn't contributing to social or environmental harm. I also wanted to avoid the FAANG companies because Big Tech gives me the heebie jeebies.

<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
<script type="text/javascript">
  google.charts.load('current', {'packages':['sankey']});
  google.charts.setOnLoadCallback(drawChart);

  function drawChart() {
    var data = new google.visualization.DataTable();
    data.addColumn('string', 'Source');
    data.addColumn('string', 'Destination');
    data.addColumn('number', 'Value');
    data.addRows([
      ['They Contacted Me (2)', 'Applications (21)', 2],
      ['I Applied (19)', 'Applications (21)', 19],
      ['Applications (21)', 'No Response (8)', 8],
      ['Applications (21)', 'Application Declined (8)', 8],
      ['Applications (21)', 'Interviews (5)', 5],
      ['Interviews (5)', 'Rejected (2)', 2],
      ['Interviews (5)', 'Offer (1)', 1],
      ['Interviews (5)', 'Incomplete (2)', 2]
    ]);

    var options = {
      sankey: {
        node: {
          label: {
            fontSize: 12
          },
          nodePadding: 20  // Increase the padding between nodes
        },
        link: {
          colorMode: 'gradient'
        }
      }
    };

    var chart = new google.visualization.Sankey(document.getElementById('sankey_chart'));
    chart.draw(data, options);
  }
</script>

<div id="sankey_chart" style="width: 100%; height: 500px;"></div>

My job search began in mid January and concluded in early April after I accepted the first offer I received (because it was good, not because I was desperate, I swear). As you can see in the Sankey diagram above, I applied to a total of 21 organizations. Two of these reached out to me directly on LinkedIn based on my profile having the `#opentowork` tag enabled. The rest I applied to via job listings I saw on [RubyOnRemote](https://rubyonremote.com/) and [HackerNews](https://news.ycombinator.com/).

What surprised me the most about finding a job in 2025 was how slow the process was. My previous experience had been spending no more than three weeks between the time I applied and the time I was given a pass or an offer. I also had gone through no more than four interviews per position. As it turns out, at least for the level of job I was seeking this time around, those numbers no longer held. To earn the offer I accepted, I faced nine one-on-one interviews over the course of ten weeks as well as seven phone conversations with a recruiter. This seemed like a lot to me.

First, I'll cover the interviews that did not result in an offer.
<br>
<br>

![Header image depicting a robot psychiatrist](/assets/images/posts/2025-04-06/hospital.jpg)

## The Small Health Startup

The first set of interviews I completed was at a startup that provided web-based patient management solutions for small businesses focused on mental health, primarily psychiatry practices. The tech stack included Rails and Ember.js, a frontend framework that I was unfamiliar with but open to learning. I applied to their job posting for a Senior Software Engineer role on [RubyOnRemote](https://rubyonremote.com/) and heard back from the CTO about two weeks later via email. He informed me that their process included five stages over the course of two to three weeks that would evaluate my technical abilities and soft skills. All conversations were conducted over Zoom with video enabled.

The first conversation was with an engineering manager that lasted one hour. The first half focused on my work history and experience and the second half was a light tech screening. The questions covered basic knowledge of topics such as APIs, web hooks, database transactions, rate limiting, etc. The questions were very general and easy to answer, appropriate for a basic screening. I was able to ascertain from the manager that the company consisted of about ten engineers and ten other staff and that they were only hiring one or two more engineers at the time and didn't have plans to scale up the team significantly.

The second conversation was with one of the co-founders, the CTO, and lasted one hour. The first half focused on my work history and technology experience. I also had an opportunity to ask a few questions about the business. The second half focused on a coding challenge where I shared my screen and wrote some Ruby to demonstrate my knowledge of data structures and algorithms. The first part involved writing a class that would be given an array of strings on construction and would expose a public method that would take a string and return whether it was included in the original array or not. The challenge was to implement the internal data structure such that it would be an efficient lookup when the public method was called, while the constructor could be more computationally  intensive. I should have immediately utilized `index_by` on the array in the constructor, converting it to a hash, which has O(1) lookup time. However, I stumbled on the solution initially because I had failed to understand the instructions concerning the constructor being able to do "heavy lifting." Once that was clarified, I was able to implement the class appropriately. I ran through some examples rather than writing assert-based tests, which I later realized was suboptimal. I should have written out an `assert` method and given expectations rather than verifying the output by hand, which would have better demonstrated a test driven approach.

After implementing the first part, the next challenge was to allow wildcard lookups by accepting an asterisk in place of any character in the string provided to the public method. Although we were nearly out of time at this point, I theorized about using regular expressions before settling on a multi-dimensional hash with keys being individual characters from the given strings. In any case, I didn't have time to implement any logic.

After the interview concluded, I knew I hadn't done a stellar job. I should have more closely listened to the requirements, which were given verbally, and I should have written assert-based tests first. I kept these items in mind for future interviews.

Despite my lackluster performance in that interview, the CTO said he wanted to proceed with the next stage, which invovled a take-home timed coding challenge. I was given four hours to complete a simple command line program that simulated an ATM. Three Ruby classes and JSON files were provided to define the basic architecture of the program as well as prime it with data. I used ChatGPT to build out the classes more quickly than I could have typed them by hand. As is often the case with code generated by LLMs, the initial code provided did not separate concerns into their respective classes very cleanly, so I iterated until I had clean readable code with everything in the right spot. I then had ChatGPT generate some specs in rspec, which was not a requirement of the coding challenge, but I wanted to demonstrate the importance I place on testing. I've struggled with finding an effective approach for CLI integration testing in Ruby, so I opted for class-based unit tests instead. Again, the initial specs generated by the LLM were not great, so I spent a few minutes refining and expanding them. I then ran through various manual tests against the CLI, verifying that everything worked. Finally, I improved the user experience by adding emojis and providing extra feedback on various events. I submitted the challenge after 2.5 hours instead of taking the full four hours, hoping that providing the answer early would score some additional points. The CTO responded positively, saying my code was clean, readable, and that going the extra mile with the specs was appreciated. I felt good about the challenge and looked forward to the next stages.

Here's what the CLI portion of my solution looked like:

```ruby
require_relative "lib/account"
require_relative "lib/register"
require_relative "lib/automated_teller_machine"

atm = AutomatedTellerMachine.new

def prompt_account_number
  print "### Super Secure ATM ###\nEnter account number (or 'exit') 👉 "
  gets.strip
end

def display_menu
  puts <<~MENU
    1. Show Balance
    2. Withdraw Cash
    3. Return
  MENU
  print "👉 "
end

def formatted_currency(amount)
  format("%.2f", amount).reverse.gsub(/(\d{3})(?=\d)/, "\\1,").reverse
end

def show_balance(account)
  puts "Current balance: $#{formatted_currency(account.balance)}"
end

def withdraw_cash(atm, account)
  print "Enter amount 👉 "
  amount = gets.strip

  if amount !~ /^\d+$/ || amount.to_i <= 0
    puts "❌ You must enter whole dollar amounts."
    return
  end

  process_withdrawal(atm, account, amount.to_i)
end

def process_withdrawal(atm, account, amount)
  cash = atm.process_withdrawal(account, amount)
  puts "Dispensed: #{cash.map { |denom, count| "$#{denom} x#{count}" }.join(", ") }"
  puts "New balance: $#{formatted_currency(account.balance)}"

rescue AutomatedTellerMachine::WithdrawalLimitExceeded,
        AutomatedTellerMachine::InsufficientFunds,
        AutomatedTellerMachine::InsufficientBills => e
  puts "❌ #{e.message}"
end

def show_register_balance(atm)
  register = atm.instance_variable_get(:@register)
  puts "### Admin Report ###"
  puts "Total cash: $#{formatted_currency(register.total_amount)}"
  puts "Bills available:"
  register.remaining_bills.each { |denom, count| puts "$#{denom}: #{count}" }
end

loop do
  account_number = prompt_account_number
  break if account_number.eql?("exit")

  if account_number.downcase == "admin"
    show_register_balance(atm)
    next
  end

  account = atm.find_account(account_number)
  if account
    loop do
      display_menu
      case gets.strip
      when "1" then show_balance(account)
      when "2" then withdraw_cash(atm, account)
      when "3" then break
      else puts "❌ Invalid command!"
      end
    end
  else
    puts "❌ Could not find account for '#{account_number}'!"
  end
end
```

The fourth stage involved a one hour conversation with two engineers who had been with the company for over two years. I discussed my work history and tech experience, then asked about the company culture and specific technologies they used. There seemed to be a lot of alignment right away. They asked a few questions that probed into my technical knowledge and how I had worked in teams at previous jobs. The engineers seemed kind and humble and there were no difficult gotcha questions. I got the impression that they liked my responses and I came away from this stage feeling optimistic.

The fifth and final stage was a one hour conversation with the second co-founder, who oversaw marketing and business development. Things started off on the wrong foot when he called me "Jason" rather than "Justin." Given that names are displayed on-screen in Zoom calls, I found this not only unprofessional but surprising. But, hey, not a big deal. I politely corrected him but he didn't acknowledge the correction or apologize. Again, not a big deal, but not exactly setting the best vibe for an interview. As with previous calls, I went through my work history but avoided delving into technical areas given his focus on non-technical areas. He asked me questions about interfacing with non-technical teams in my past roles. I think my answers showed strength in cross-team collaboration, as I've often been one of the few engineers willing to work effectively with marketing and sales teams in previous roles. At the end of the conversation I asked about the business and the work environment. While the vibe of the interview was dry compared to the previous conversations, I came away thinking I had a shot at an offer.

A few days later, I received an email from the CTO saying that while he thought I would have been a good fit for the role, the team had decided on another candidate. He thanked me for going through their process and wished me luck on my search. I was disappointed to receive this notice, but not entirely surprised. In hindsight, I should have performed better in the initial code challenge and that is likely what set me back from being selected. I also had a feeling that the second co-founder just didn't like me for whatever reason and/or already decided on another person for the position before interviewing me. I'll never know.

Although I didn't succeed in obtaining an offer from this company, I came away armed with knowledge for future interviews. First, I decided that in future coding challenges I would demonstrate test driven development by writing specs before implementing the logic. Second, I would ask about edge cases and seek more clarification on requirements. Third, I had improved my career storytelling skills.
<br>
<br>

![Header image depicting a cannibis leaf and computer code](/assets/images/posts/2025-04-06/cannabis.jpg)

## The Mid-Sized Cannabis Company

Given my seven year stint at Weedmaps, a cannabis aggregation platform, when I saw that one of their main competitors was hiring, I applied. In my cover letter, I included a paragraph about my experience at Weedmaps and how that could be leveraged to help them achieve similar goals. Like Weedmaps, their tech stack was based on Ruby on Rails, so it seemed like a good fit for me. I got a response from a recruiter within two days, so I think my experience in the cannabis industry caught their eye.

The recruiter informed me that the interview process would include five stages over the course of four weeks, which was similar to the process at the health care company. It seemed there would be only one coding challenge stage and the rest would be discussions with engineering leaders, focusing more on soft skills and culture fit. All of the conversations would be done over Google Meet with video enabled.

The first conversation took place with the VP of Engineering and lasted one hour. We talked about my work history, company goals and culture, as well as music. One of my main side projects ([Phish.in'](/projectes/02-phishin.html)) is a popular streaming site among Phish fans, which I discussed. The VP happened to be wearing a Dave Mathews Band hoody, which indicated a kind of culture I thrive in. After my failure at obtaining an offer on my previous interviews, I let the VP know that although I had a ton of experience building Rails systems both on and off the job, I wasn't always great at technical interviews. Although I was applying for a Staff level role, I said I would also be open to a Senior role if I didn't evaluate highly enough. In hindsight, I should have exuded more confidence and held my cards closer to the chest. I erred on the side of humility, which I think was a mistake.

The second round consisted of a coding challenge with two engineers: a Staff-level engineer with several years at the company and a Mid-level engineer who had been there six months. The challenge took place in CodePen, which surprisingly included a dedicated ChatGPT tab. I faced a dilemma—should I demonstrate my own coding abilities or use AI to generate a quick solution as I might in a real-world scenario? Despite the temptation, I chose to solve the problem independently, hoping to impress the interviewers with my technical skills rather than my prompt "engineering."

The challenge was to create a Ruby class that allowed customers to check in and out based on their unique ID and business type. The class had to provide public methods for `checkin`, `checkout`, and `average_time`. The latter method had to calculate the average time checked in across all customers for a given type within the last week. Test code was provided with the requirements. This code included `sleep` calls to simulate the passage of time, which slowed down the execution. I found this approach surprising and a little shoddy. I made an off-hand joke about this approach as I waited for their code to run once I had built a solution, saying "you gotta love sleeps in specs." In hindsight, this may have been considered rude rather than a friendly joke, although I can't be sure. My code worked and they verified that the output was correct. The Staff engineer asked about a requirement that I had missed, which was that the average should include only checkins that happened within the last week. I had accidentally skipped over this requirement given that all of the actual checkins happened over the course of a few seconds so filtering out anything older than a week wouldn't change the output. Still, this was my fault and clearly a mistake. To save time, I turned to the ChatGPT tab to give me the code to filter out old checkins, and added it to my class. I ended up producing a working answer in about 20 minutes and then had an opportunity to ask them a few questions about the company and what it was like to work there. Afterwards, we still had ten minutes left in the hour, but I didn't have any additional questions, and confirmed that they didn't have any additional coding challenges, so we ended the session early.

Here's an approximation of the solution I gave:

```ruby
class CheckInSystem
  TYPES = %w[medical recreational]

  def initialize
    @check_ins = {}
    @check_in_history = {}
  end

  def checkin(id, type)
    raise ArgumentError, "Invalid type" unless type.in?(TYPES)
    raise "Customer #{id} is already checked in" if @check_ins.key?(id)

    @check_ins[id] = {
      checkin: Time.now,
      type: type
    }
  end

  def checkout(id)
    raise "Customer #{id} is not checked in" unless @check_ins.key?(id)

    check_in_data = @check_ins[id]
    duration = Time.now - check_in_data[:checkin]
    type = check_in_data[:type]

    @check_in_history[type] ||= []
    @check_in_history[type] << duration

    @check_ins.delete(id)
  end

  def average_time(type)
    raise ArgumentError, "Invalid type" unless type.in?(TYPES)
    return 0 if !@check_in_history.key?(type) || @check_in_history[type].empty?

    one_week_ago = Time.now - 7*24*60*60
    recent_durations = @check_in_history[type].select do |duration|
      duration[:time] > one_week_ago
    end

    return 0 if recent_durations.empty?
    recent_durations.sum / recent_durations.length
  end
end
```

I came away thinking that it was an odd interview but an easy one. I had solved the problem in a memory efficient way by saving only the time a customer had been checked in rather than the checkin type, start, and end, for every historical checkin. Their specs did not demonstrate a customer checking in more than once, so I had assumed that keeping a history of all checkin times would be a waste of memory. However, in hindsight, based on some comments from the Staff engineer near the end of the challenge, they may have been looking for a persistent storage pattern. I should have asked them about this kind of edge case and written assert-based specs before diving into a solution. Despite this, I assumed that because my solution worked and was efficient (while barely touching the AI tab), that I would be proceeding to the next round of interviewing. Unfortunately, that was not the case.

After not hearing back from the recruiter for over a week, I contacted them and received a response from another recruiter saying that they had decided not to proceed with the next round based on my performance in the coding challenge. They also said that they unfortunately could not provide any specific feedback on how I could have done better. I was surprised and disappointed as I thought I had done at least an adequate job. I came away from this one feeling confused.
<br>
<br>

![Header image depicting stacks of coins](/assets/images/posts/2025-04-06/money.jpg)
## The Growing Payroll Company

The interview process that finally resulted in an offer began with a recruiter reaching out to me on LinkedIn. Incidentally, a few days prior I had applied for the Staff Software Engineer role advertised on [RubyOnRemote](https://rubyonremote.com/), so I let the recruiter know and he looked up my application. This led to a one hour phone screen with the recruiter that covered my work history, technical experience, salary expectations, and career aspirations. He let me know that their process would take several weeks and included several stages, although he was not more specific than that at the time. The role sounded like a good fit for me so I agreed to proceed. The recruiter informed me that their coding challenges were difficult and that I should study medium and hard level problems on [LeetCode](https://leetcode.com/). I asked for a couple of weeks before my first interview so I could study and he agreed.

I spent the next two weeks working through problems on LeetCode and CodeSignal, similar sites that both provide users with coding challenges that strengthen knowledge of data structures and algorithms. This style of challenge was not my forte because I had not taken Computer Science in college, but rather Information Technology. While I had learned a lot of CS  fundamentals on the job while building web apps during my career, I had never delved deeply into how various data structures worked under the hood and how memory and time efficiency worked at a low level. Working through the challenges those two weeks was fun but also daunting. The hard level problems on LeetCode I found to be intractable and I had to look up the answers and try to grok the underlying lessons. In hindsight, I should have done these types of challenges earlier in my career. Although a lot of the problems had little to do with the actual products I had been building throughout my professional life, understanding the solutions boosted my ability to think critically about efficient and readable code. I was nervous about how I might perform in the interviews but I decided to do my best and proceed.

The first interview was a technical screen via Zoom with a frontend engineer. The coding was done in CodeSignal. The challenge was given in writing and AI assistance was not permitted. Instead of a hardcore problem like the one I had been working on the last two weeks, it was related to payroll, which I found refreshing. I had to write a single method that would take a hash of employees with keys being names and values being amount owed, plus an integer representing total amount available. The method was supposed to pay each employee as evenly as possible in the case where there was insufficient money. Armed with my previous experience, I asked for edge cases up front before I began writing any code. I also wrote out a few test cases, although they were not assert-based (this interview actually occurred early in my job search - I had not yet learned the lessons mentioned earlier). I produced a correct answer within about half an hour and we ran through some edge cases. An additional challenge was added which specified that employees should be sorted by name and favored in the case where there were not enough funds to pay full amounts. My solution to this included sorting the employee hash (in Ruby, this converts the hash to an array of arrays) and then converting it back to a hash. In hindsight, I should have stuck with an array, as converting back to a hash was a waste of compute and memory. The engineer was hinting at there being a more optimal solution, but, not knowing Ruby (he was a JavaScript engineer), he couldn't (or wouldn't) say exactly. He ended up giving me an additional 15 minutes over the hour to ask him questions about the company and what it was like to work there. Overall I came away from the experience feeling positive, but not certain I did a good enough job on the technical solution to proceed.

Here's an approximation of my solution for this challenge:

```ruby
def distribute_pay(employee_debts, total_available)
 sorted_employees = employee_debts.sort_by { |name, _| name }
 total_debt = employee_debts.values.sum
 payments = {}

 if total_available >= total_debt
   employee_debts.each do |name, owed|
     payments[name] = owed
   end

   return payments
 end

 base_amount = total_available / sorted_employees.length
 remainder = total_available % sorted_employees.length
 amount_left = total_available
 sorted_employees.each_with_index do |(name, owed), index|
   extra = index < remainder ? 1 : 0
   payment = [owed, base_amount + extra].min
   payments[name] = payment
   amount_left -= payment
 end

 payments
end
```

A few days later I got a call from the recruiter congratulating me on passing the technical screen. He also gave me some valuable feedback. He said in future coding sessions, I should focus more on writing robust pass/fail tests before I jump into the solution and that I should cover all possible edge cases in my specs so that when it came to writing the code itself, there would be no questions about requirements. This was very valuable feedback that I carried forward to the rest of my interviews. The recruiter informed me that the next step would be a "virtual onsite," which would consist of five one-on-one interviews, three of which would be technical, and two focusing on soft skills. Because of a company wide conference that was occurring the following week, these interviews didn't get scheduled until two weeks later. The virtual onsite would involve conversations via Zoom with video enabled. Coding challenges would be completed on CodeSignal.

My first interview of the virtual onsite was a half hour value alignment conversation with a non-technical employee. We talked about my past work history, my values, and my career goals. Strangely, I began losing my voice during this interview, which almost never happens to me. I didn't feel especially nervous but for some reason my vocal cords did not want to cooperate. My interviewer was very understanding as I kept breaking for sips of water. I thought my answers to her questions were good, but I felt like my voice may have indicated a lack of confidence. I just hoped that my voice would hold up for the longer technical interviews that were scheduled just an hour later. Between interviews, I brewed hot tea to soothe my voice for the upcoming session. This seemed to solve the problem.

The second interview was an hour in length focusing on another coding challenge. It was moderately more difficult than the technical screen in that it involved writing a class rather than a single method. The class had to implement a key/value store with `set`, `get`, and `delete` methods as well as keeping a history of values and the timestamps when they were set. The `get` method could optionally accept a timestamp and the method would need to return the value associated with that timestamp, even if the timestamp didn't exactly match the time when the value was set. Taking the recruiter's feedback into account, I spent a few minutes writing a robust set of pass/fail tests and asked about a variety of edge cases, ensuring that my test suite was robust. I then produced a solution that used sub-hashes to store timestamps and values. After the interview when I had more time to think about the solution, I realized that I should have used an array instead and that the `get` method should have used a binary search to efficiently find the appropriate value for a given timestamp. Instead, I implemented a slower linear scan across hash keys.

The third interview was a discussion with an engineering leader at the company who had been there for almost a year. We discussed my work history, technical experience, side projects, and the impact of AI on programming. The conversation went smoothly and I was given an opportunity to ask him about what it was like working at the company. It seemed like a friendly kind of corporate place.

The fourth interview tested my knowledge of web architecture. They showed me mockups of a survey creation interface where users could design questionnaires with custom questions and options, then publish them for their followers to complete. The challenge was to design an architecture that could handle a survey from a celebrity who had millions of followers, all of whom would submit responses simultaneously. First I designed the database schema, demonstrating my knowledge of ActiveRecord and relational databases. After a few minutes, the interviewer said that what I had was fine and that she didn't need to see a complete database schema, but that I should focus instead on the architectural elements. I started with the write side. I explained that ultimately the database would be the bottleneck so you would need to ensure sufficient vertical scale. Database sharding could be implemented especially for users who had many followers so that more physical resources could be assigned to them. Also, a durable queuing mechanism could be placed between the database and the web boxes with a parallelized asynchronous processing system to ensure eventual consistency. Finally, web servers would need sufficient horizontal scaling with load balancing to handle the high volume of API requests. After talking about the writes, the interviewer asked about the read side, which, admittedly, I should have talked about first. I explained that, again, the database would be the most concerning bottleneck, so read replicas could be setup to accommodate large amounts of traffic. Similarly for writes, web boxes would need to be sufficiently horizontally scaled to handle the API requests from clients. Additionally, caching could be done at the web layer to reduce hits on the database. I concluded by saying that boring and reliable technologies usually trump shiny and new when it comes to architecture and code.

The fifth interview was another coding challenge focusing on tax bracket calculations. I was given a link to an IRS web page that displays the income-based federal tax brackets. I was asked to implement a Ruby class that would encapsulate this data and calculate a taxpayer's total liability given their income. As before, I started by writing a robust set of specs, asking about edge cases and ensuring that I clearly understood the requirements. The interviewer helped fill in my expected test values using a spreadsheet that contained a working solution (not shared with me). My solution involved a hash constant to specify the bracket values from the IRS website and a method that looped through these brackets, adding up the liability for each chunk of the total income of the given taxpayer, returning the total liability. Once all of the tests passed, the interviewer asked about how I might expand my solution to accommodate multiple years and how I might store multi-year bracket data. I discussed a few options and the tradeoffs involved.

Here's an approximation of what the code looked like:

```ruby
class TaxCalculator
  TAX_BRACKETS = [
    [0, 0.10],
    [10275, 0.12],
    [41775, 0.22],
    [89075, 0.24],
    [170050, 0.32],
    [215950, 0.35],
    [539900, 0.37]
  ].freeze

  def calculate_tax(income)
    return 0 if income <= 0

    total_tax = 0
    TAX_BRACKETS.each_with_index do |(threshold, rate), index|
      next_threshold = TAX_BRACKETS[index + 1]&.first || Float::INFINITY
      return total_tax unless income > threshold
      taxable_in_bracket = [income, next_threshold].min - threshold
      total_tax += taxable_in_bracket * rate
    end
  end
end

def expect(id, actual, expected)
  raise "Failure on #{id}: #{actual}" unless actual == expected
end

actual = TaxCalculator.new.calculate_tax(21_322)
expect("Test 1", actual, 13_591)

...

puts "PASS"
```

About a week after the virtual onsite, my recruiter said he was still waiting for results, and about two weeks later he confirmed that they had decided to proceed with my candidacy. I was six weeks into the process at this point. The next (and what I assumed would be the final) step was talking with an engineering manager about a specific role. The zoom conversation was similar to previous ones in that I gave a brief history of my career focusing on my technical strengths. I was then able to ask the manager about specifics of the role. I thought the conversation went well and I was looking forward to a potential offer at this point.

I emailed the recruiter saying I enjoyed the conversation and that I felt alignment with the job. The recruiter responded by email saying that unfortunately the role had been filled by another candidate but he was going to get me in touch with another similar team, so he setup another half hour Zoom call with the manager.

This call went exceptionally well. The manager and I had a good conversation about tech of all kinds and we seemed to have good alignment on modern topics like cryptocurrency and AI. The convo was going so well that we even extended it by fifteen minutes. At the end of the call, the manager indicated that she was going to reach out to my recruiter right away, indicating positive feedback. After the call I thought for sure an offer would be forthcoming.

A week went by without hearing from the recruiter. I finally reached out but it took him several more days to respond, which I found troubling. We setup a call and in it he apologized for the lack of response and explained he had been very busy the previous week with other tasks. He said he had some good news and some bad news. The bad news was that the role I had last interviewed for had been filled but the good news was that he was going to get me in touch with yet another team.

So, I went on to my ninth interview. This one was a half hour zoom call with the manager of a team that worked on their main line of products. The conversation went well, but not as well as the previous two calls. There seemed to be a lack of enthusiasm and alignment, although the role was still interesting to me and I maintained an upbeat attitude during the call. I figured if I had not been selected for the previous two roles, I would not be selected for this one either.

A few days later, I received a call from the recruiter saying that the manager had given me a glowing review and wanted to extend an offer that exceeded my previous salary as a Staff engineer by more than 10%. After what seemed like an endless Kafakaesque process, I had finally found a well paying job that would utilize my existing expertise. Success!
<br>
<br>

![Header image depicting frayed rope](/assets/images/posts/2025-04-06/vines.jpg)

## Loose Ends

While I was interviewing with the payroll company, a commercial building consulting firm reached out to me on LinkedIn. I talked with the CTO over Zoom for 45 minutes. The company was a new startup based in San Francisco that was focused on reducing CO2 emissions related to commercial real estate. This interested me from a cultural perspective. The conversation went well and I was scheduled for a followup technical interview where I was asked to bring my own project and my own task to demonstrate my knowledge of Ruby on Rails. As the maintainer of a popular Rails open source project, I already had several tasks on my to-do list, making this challenge perfect — I could showcase my skills while improving a side project. Incidentally, I ended up accepting the offer from the payroll company and thus canceled the interview.

I also received a response from one of my applications to a company that provided team email and chat. The email expressed interest in proceeding with a conversation with the CTO and included a series of questions that I would be expected to answer. I appreciated the openness of this approach as well - it's rare that you get to see the specific questions you'll be asked in an interview ahead of time. However, given that I had already accepted an offer, I had to decline.

## Takeaways

It had been about a decade since I had interviewed for a software engineering job before this. In my previous experience, the process did not last as long, did not involve so many technical rounds, and did not involve me explaining my work history repeatedly. I was also surprised to have less than a 30% positive response rate on my specifically targeted applications, which made me question the quality of my resume.

If you are an engineer seeking a job, remember: don't give up! Even if you receive multiple rejections, stay confident that there's an org out there where you will fit in. Each interview you do strengthens your ability to perform better next time. Stay confident and positive. Eventually you'll find your next role.
<br>
<br>

![Footer image depicting office cubicles](/assets/images/posts/2025-04-06/cubicles.jpg)

