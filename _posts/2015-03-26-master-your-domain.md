---
layout: post
title: "Master Your Domain with Swift"
description: ""
summary: "In programing we're mostly just taking some input and producing some output. Wether we're talking about gestures on a screen, processing a photo with some Core Image filters, or just formatting some text. One important aspect of this and an area where we sometimes get a little lazy, is in considering the domain, or the set of *valid* inputs."
category: iOS
tags: [swift]
---
{% include JB/setup %}
***domain**:  the set of "input" or argument values for which [a] function is defined.
— [Wikipedia: "Domain of a Function"](http://en.wikipedia.org/wiki/Domain_of_a_function)*

In programing we're mostly just taking some input and producing some output. Wether we're talking about gestures on a screen, processing a photo with some Core Image filters, or just formatting some text. One important aspect of this and an area where we sometimes get a little lazy, is in considering the domain, or the set of *valid* inputs. In Objective-C laziness in this regard is almost encouraged by the fact that `nil` is "valid" in a lot of cases where it maybe shouldn't be; after all, you can send any message you like to `nil` and you'll get a reasonable response every time. The problem is that this can lead to some nasty bugs.

    @interface Assignment: NSObject
        // nil if there is no due date
        @property NSDate *dueDate;
    @end

A few months and one feature request later:

    Assignment *a = self.assignments[indexPath.row];
    cell.detailTextLabel.text = [self.dateFormatter stringFromDate:a.dueDate];

💥**CRASH!**💥

`NSDateFormatter`'s `stringFromDate:` does not like `nil`.

Swift has given us the abilty to tighten things up a little bit by making a parameter like this non-`Optional`.

    struct Assignment {
        let dueDate: NSDate
    }

Thisw will likely prevent the crashing problem, but it leads to a different problem: what if there is no due date? One option would be to just make `dueDate` optional like so:

    let dueDate: NSDate?
    
But more and more I find myself using `enum`s to be very explicit about what the valid values are for a particular property, variable, or argument.

    struct Assignment {
        enum Due {
            case NoDueDate
            case Date(NSDate)
        }
    
        let due: Due
    }

Now the set of possible values, the domain for an assignment's due status, is very clearly specified and `nil` is no longer an option. We are very explicit about how we represent assignments with no due date, and as an added bonus we can delegate the responsibility of formatting the due date to `Assignment.Due`:

    extension Assignment.Due: Printable {
        var description: String {
            switch self {
            case .NoDueDate:
                return noDueDateDescription
            case .Date(let date):
                return formatter.stringFromDate(date)
            }
        }
    }

With Swift's `enum`s we can put a little bit tighter bounds on the valid inputs our functions are defined for and thus become masters of our domain.

