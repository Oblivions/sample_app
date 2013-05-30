 # == Schema Information
#
# Table name: Users
#
# id :integer not null, primary key
# name :string(255)
# email :string(255)
# created_at :datetime not null
# updated_at :datetime not null
#

require 'spec_helper'

describe User do
before do
@User = User.new(name: "Michael Hartl", email: "mhartl@example.com")
end

subject {@User}

it {should respond_to(:name)}
it {should respond_to(:email)}

it {should be_valid}

describe "when name is not present" do
before {@User.name = " "}
it {should_not be_valid}
end 

describe "when email is not present" do
before {@User.email = " "}
it {should_not be_valid}
end 

describe "when name is too long" do
before {@User.name = "a"*51}
it {should_not be_valid}
end 

describe "when email format is invalid" do
it "should be invalid"do
addresses = %w[user@foo,com user_at_foo.org example.user@foo. foo@bar_baz.com foo@bar+baz.com]
addresses.each do |invalid_address|
@User.email = invalid_address
@User.should_not be_valid
end
end
end

describe "when email format is valid" do
it "should be invalid" do
addresses = %w[user@foo.com A_US-ER@f.b.org frst.lst@foo.jp a+b@baz.cn]
addresses.each do |valid_address|
@User.email = valid_address
@User.should be_valid
end
end
end

describe "when password confirmation is nil" do
    before do
      @user = User.new(name: "Michael Hartl", email: "mhartl@example.com",
                       password: "foobar", password_confirmation: nil)
    end
    it { should_not be_valid }
  end

  describe "with a password that's too short" do
    before { @user.password = @user.password_confirmation = "a" * 5 }
    it { should be_invalid }
  end

  describe "return value of authenticate method" do
    before { @user.save }
    let(:found_user) { User.find_by(email: @user.email) }

    describe "with valid password" do
      it { should eq found_user.authenticate(@user.password) }
    end

    describe "with invalid password" do
      let(:user_for_invalid_password) { found_user.authenticate("invalid") }

      it { should_not eq user_for_invalid_password }
      specify { expect(user_for_invalid_password).to be_false }
    end
  end
end
